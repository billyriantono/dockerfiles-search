FROM theadrum/tomcat:jdk_7_tomcat_7
MAINTAINER Theadrum <david@wetstone.co.nz>
ENV JAVA_TOOL_OPTIONS -Dfile.encoding=UTF8
ENV CATALINA_OPTS="-Dorg.apache.tomcat.util.http.Parameters.MAX_COUNT=10240 -Djava.awt.headless=true -XX:-OmitStackTraceInFastThrow -Djava.util.Arrays.useLegacyMergeSort=true -Xms256m -Xmx4096m -XX:MaxPermSize=1024m -XX:+CMSClassUnloadingEnabled -XX:+UseConcMarkSweepGC -Dcom.sun.management.jmxremote"
RUN java -version
RUN mkdir -p /usr/terminalfour/www
RUN mkdir -p /usr/terminalfour/contentstore
ADD http://dropbox.wetstone.co.nz/public/jdbc/mysql-connector-java-5.1.26-bin.jar /opt/apache-tomcat/lib/
ADD http://dropbox.wetstone.co.nz/public/jdbc/sqlite-jdbc-3.7.2.jar /opt/apache-tomcat/lib/
ADD http://dropbox.wetstone.co.nz/public/jdbc/postgresql-9.3-1100-jdbc4.jar /opt/apache-tomcat/lib/
ADD http://dropbox.wetstone.co.nz/public/jdbc/sqljdbc41.jar /opt/apache-tomcat/lib/
COPY server.xml /opt/apache-tomcat/conf/server.xml
EXPOSE 8080
