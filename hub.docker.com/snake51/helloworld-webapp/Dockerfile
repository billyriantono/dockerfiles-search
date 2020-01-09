#déploiement d'une webapp helloworld.war sur un tomcat
FROM tomcat:jdk11-adoptopenjdk-openj9

RUN rm -rf /usr/local/tomcat/webapps/examples
COPY tomcat-users.xml /usr/local/tomcat/conf/
COPY context.xml /usr/local/tomcat/webapps/manager/META-INF
COPY context.xml /usr/local/tomcat/webapps/host-manager/META-INF

# Dépôt du war (le workdir de tomcat est déjà positionné sur /usr/var/tomcat/)
ADD hello-world.war ./webapps