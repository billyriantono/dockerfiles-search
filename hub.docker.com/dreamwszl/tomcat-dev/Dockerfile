FROM tomcat

COPY ./tomcat-users.xml /usr/local/tomcat/conf/

EXPOSE 8000
CMD ["catalina.sh", "jpda", "run"]
