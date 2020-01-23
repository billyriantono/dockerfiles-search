FROM tomcat:8.5-alpine

# Install msfonts
RUN apk --no-cache add msttcorefonts-installer fontconfig && \
    update-ms-fonts && \
    fc-cache -f

# Install tzdata
RUN apk add tzdata && \
    cp /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime && \
    echo "America/Sao_Paulo" >  /etc/timezone

# Remove default tomcat apps/docs/examples
RUN rm -rvf /usr/local/tomcat/webapps/docs
RUN rm -rvf /usr/local/tomcat/webapps/examples
RUN rm -rvf /usr/local/tomcat/webapps/ROOT

# Remove default server config
RUN rm -f /usr/local/tomcat/conf/server.xml

# Add custom server config
ADD server.xml /usr/local/tomcat/conf/server.xml
