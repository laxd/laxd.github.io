---
layout: default
title: "Spring Boot setup with repositories"
categories: spring, java
---

* Create DAOs by subclassing CrudRepository
* Get handle on entityManager with a @Bean annotated method in your main class
* Create datasource using @Bean/@ConfigurationProperties annotated method in main class (with properties prefix)
* Add spring-boot-tomcat-start to get around "No Supported DataSource type found" - This relates to BasicDataSource (etc) and NOT the datasource properties

