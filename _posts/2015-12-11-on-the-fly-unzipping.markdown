---
layout: post
title: "Saving space and time with on-the-fly unzipping"
date: 2015-12-11 14:00:00 +0000
categories: mysql unix
---

Files are often delivered in a compressed format to save bandwidth. However, this means having to unzip/untar a file before being able to use it. This often results in leftover files hanging around taking up valuable space, as well as requiring 2 steps to complete an action rather than 1 (unzip followed by whatever you want to do with the file). With a bit of unix-foo, you can get both done in one step:

Unzipping:
{% highlight bash %}
unzip -p sql_file.zip | mysql -u user
{% endhighlight %}

Untarring:
{% highlight bash %}
tar -xvf sql.tar.gz --to-command="mysql -u user"
{% endhighlight %}

This allows us to use compressed files without having to store the uncompressed file on your file system. This also works if the archive contains multiple files, as each file is piped into the given command individually.

The same principle can of course be applied in reverse, zipping output on the fly without having to store it in the file system first:
{% highlight bash %}
mysqldump -u user | gzip > database_dump.sql.gz
{% endhighlight %}
