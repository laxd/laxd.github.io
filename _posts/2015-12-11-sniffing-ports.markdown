---
layout: post
title: "Sniffing database ports for queries"
date: 2015-12-11 13:00:00 +0000
categories: mysql database
---

Having a single line of bash that can be used to list incoming queries to a database can be invaluable, especially during development when using an ORM such as Hibernate with its own version of SQL. Personally, I find the greatest benefit of sniffing the port over enabling query logging is on production systems, where you may not be able to access the database instance to enable query logging, and even if you could, wouldn’t want to for performance reasons.

This example is focused on MySQL, but the approach is completely database agnostic (as long as you can force it to use tcp instead of a socket). The command I use is:

{% highlight bash %}
sudo tcpdump -i lo -s 0 -l -w - dst port 3306 | strings
{% endhighlight %}

This breaks down as follows:

-i lo specifies the interface to listen on. For a machine on localhost, this should be the loopback interface, lo (note that your application has to connect via 127.0.0.1 and not via localhost, or it will use a socket that can’t be sniffed). For externally originating queries, use eth0 or equivalent.

-s 0 tells tcpdump how many bytes to sniff from each packet. If left blank, this defaults to 116. Usually you would limit the bytes to the shortest you can, but as we don't know how long our query will be, we set this to unlimited.

-l line buffers the output. E.g. once it reaches the end of a line it will send it to stdout rather than waiting. Using this allows us to pipe the output directly into other commands such as grep.

-w writes the output to a file. In this case, the argument following -w is a dash (“-“), indicating output should be sent to stdout. Without this argument, tcpdump would parse the packets and output the packet information instead of the query string, which isn’t particularly useful in this use case.

dst port 3306 is the criteria on which to select packages from. For this example, we will only see packets that have been sent to port 3306 (as dst is destination), and we won’t see the replies from MySQL.

Finally, we pipe the output into strings to convert the individual character codes into text that we can understand.

As mentioned above, what I find really useful is being able to grep through the results as they come in. Piping the results through a filter that only displays, for example,
insert queries, or queries containing an ID that you know will be used can really help in narrowing down your query.
