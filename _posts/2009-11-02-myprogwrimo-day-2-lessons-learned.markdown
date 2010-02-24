--- 
wordpress_id: 394
layout: post
title: MyProgWriMo - Day 2 - Lessons Learned
wordpress_url: http://tragicallyleet.com/?p=394
---
This is going to be harder and easier than I thought.

So Tapestry supplies its own IoC container, so no Spring at this point. Also there is a nice Hibernate integration, so I am starting to mess with my entities and figure out the needed annotations.

Maven profiles seem to manage the different configuration aspects of my application such as properties for development versus a Hudson build.  So I can find it in the future, here is the profile snippet for development with a in memory database:

[sourcecode lang="xml"]
        <profile>
            <id>development</id>
            <properties>
                <hibernate.dialect>org.hibernate.dialect.HSQLDialect</hibernate.dialect>
                <hibernate.connection.driver_class>org.hsqldb.jdbcDriver</hibernate.connection.driver_class>
                <hibernate.connection.url>jdbc:hsqldb:mem:autoblog</hibernate.connection.url>
                <hibernate.connection.username>sa</hibernate.connection.username>
                <hibernate.connection.password></hibernate.connection.password>
                <hibernate.connection.pool_size></hibernate.connection.pool_size>
                <hibernate.connection.autocommit>true</hibernate.connection.autocommit>
                <hibernate.cache.provider_class>org.hibernate.cache.HashtableCacheProvider
                </hibernate.cache.provider_class>
                <hibernate.hbm2ddl.auto>create-drop</hibernate.hbm2ddl.auto>
                <hibernate.show_sql>true</hibernate.show_sql>
            </properties>
        </profile>
[/sourcecode]
