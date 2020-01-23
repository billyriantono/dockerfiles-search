FROM tomcat:9.0.13-jre11-slim

RUN apt update;apt install -y curl
RUN mkdir /var/lib/birt_reports
RUN curl -LO http://ftp.osuosl.org/pub/eclipse/birt/downloads/drops/R-R1-4.8.0-201806261756/birt-runtime-4.8.0-20180626.zip&&unzip birt-runtime-4.8.0-20180626.zip birt.war -d /tmp&&unzip /tmp/birt.war -d /usr/local/tomcat/webapps/birt&&rm /tmp/birt.war birt-runtime-4.8.0-20180626.zip
RUN curl -o /usr/local/tomcat/lib/sqlite-jdbc-3.25.2.jar -L https://search.maven.org/remotecontent?filepath=org/xerial/sqlite-jdbc/3.25.2/sqlite-jdbc-3.25.2.jar
RUN curl -o /usr/local/tomcat/lib/mssql-jdbc-7.0.0.jre8.jar -L https://search.maven.org/remotecontent?filepath=com/microsoft/sqlserver/mssql-jdbc/7.0.0.jre8/mssql-jdbc-7.0.0.jre8.jar
ADD web.xml /usr/local/tomcat/webapps/birt/WEB-INF/web.xml
VOLUME ["/var/lib/birt_reports"]