#此版本結合was 與 sqlserver JNDI設定
#user: wsadmin
#password: p@ssw0rd
#JNDI name: jdbc/ccdb3

#binding sqlserver info:
#host: sqlserver
#user: sa
#password: p@ssw0rd


# source setting
FROM ibmcom/websphere-traditional:8.5.5.9-profile
MAINTAINER AndyChen iisi.com

#add files with jndi setting

# login DB settings
ADD security.xml /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/config/cells/DefaultCell01

# jdbc provider and jndi settings
ADD resources.xml /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/config/cells/DefaultCell01/nodes/DefaultNode01/servers/server1

# sqlserver jar path
ADD variables.xml /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/config/cells/DefaultCell01/nodes/DefaultNode01/servers/server1

# jar file import
ADD sqljdbc4.jar /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/libs/sqljdbc4.jar

# open server debugger mode
ADD server.xml /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/config/cells/DefaultCell01/nodes/DefaultNode01/servers/server1

# add orignal wsadmin password as p@ssw0rd
ADD PASSWORD /tmp

# create fake D with project
# add an empty folder 
COPY folderToServer/D/ /opt/IBM/WebSphere/AppServer/profiles/AppSrv01

# link D to D: 
RUN ln -s /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/D /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/D:

# Set the locale
ENV LANG C.UTF-8
ENV LANGUAGE en_US:en  
ENV LC_ALL C.UTF-8

# open port
EXPOSE 9443
EXPOSE 9043
EXPOSE 7777