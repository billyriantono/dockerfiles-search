FROM mikolajr/docker-tomcat:8.5.24
MAINTAINER Mikolaj Rydzewski <mikolaj.rydzewski@gmail.com>

ADD http://www.apache.org/dist/jspwiki/2.10.5/binaries/webapp/JSPWiki.war /tmp
ADD http://www.apache.org/dist/jspwiki/2.10.5/wikipages/jspwiki-wikipages-en-2.10.5.zip /tmp

RUN \
	mkdir /usr/local/tomcat/jspwiki && \
	cd /usr/local/tomcat/jspwiki && mkdir pages logs etc work && \
	cd /usr/local/tomcat/webapps && mkdir ROOT wiki && \
	unzip -d /usr/local/tomcat/webapps/wiki /tmp/JSPWiki.war && rm /tmp/JSPWiki.war

RUN \
	cd /tmp && \
	unzip -q jspwiki-wikipages-en-2.10.5.zip && \
	mv jspwiki-wikipages-en-2.10.5/* /usr/local/tomcat/jspwiki/pages/ && \
	rm -rf jspwiki-wikipages-en-2.10.5*

RUN \
	cd /usr/local/tomcat/webapps/wiki/WEB-INF && \
	mv userdatabase.xml groupdatabase.xml /usr/local/tomcat/jspwiki/etc

ADD jspwiki.policy /usr/local/tomcat/webapps/wiki/WEB-INF
ADD index.jsp /usr/local/tomcat/webapps/ROOT

ENV LANG en_US.UTF-8
ENV jspwiki_pageProvider VersioningFileProvider
ENV jspwiki_fileSystemProvider_pageDir /usr/local/tomcat/jspwiki/pages
ENV jspwiki_basicAttachmentProvider_storageDir /usr/local/tomcat/jspwiki/pages
ENV jspwiki_workDir /usr/local/tomcat/jspwiki/work
ENV jspwiki_xmlUserDatabaseFile /usr/local/tomcat/jspwiki/etc/userdatabase.xml
ENV jspwiki_xmlGroupDatabaseFile /usr/local/tomcat/jspwiki/etc/groupdatabase.xml
ENV jspwiki_use_external_logconfig true
ENV jspwiki_templateDir haddock
ENV jspwiki_jspwiki_frontPage Main

CMD [ "bin/start_override.sh", "bin/catalina.sh", "run" ]

