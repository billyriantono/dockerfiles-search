FROM openjdk:8-jre-alpine

RUN wget -qO - https://repo1.maven.org/maven2/io/vertx/vertx-stack-manager/3.3.3/vertx-stack-manager-3.3.3-full.tar.gz | tar xvz -f - -C /usr/local

RUN apk add --update bash nginx unzip openrc && rm -rf /var/cache/apk/*
RUN chmod +x /usr/local/vertx/bin/vertx

# Configure Vert.x
ENV VERTX_HOME /usr/local/vertx
ENV PATH $VERTX_HOME/bin:$PATH
RUN wget -qP /usr/local/vertx/lib/ http://central.maven.org/maven2/org/slf4j/jcl-over-slf4j/1.7.16/jcl-over-slf4j-1.7.16.jar
RUN wget -qP /usr/local/vertx/lib/ http://central.maven.org/maven2/ch/qos/logback/logback-classic/1.2.0/logback-classic-1.2.0.jar
RUN wget -qP /usr/local/vertx/lib/ http://central.maven.org/maven2/ch/qos/logback/logback-core/1.2.0/logback-core-1.2.0.jar
RUN echo $'<configuration scan="true" debug="true">\n\
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">\n\
        <encoder>\n\
            <pattern>%d{HH:mm:ss.SSS}|%20.20thread|%-5.5level|%-36.36logger{36}|%msg%n</pattern>\n\
        </encoder>\n\
    </appender>\n\
\n\
    <root level="INFO">\n\
        <appender-ref ref="STDOUT"/>\n\
    </root>\n\
</configuration>\n' > /usr/local/vertx/conf/logback.xml

# Configure NGINX
RUN mkdir /run/nginx
RUN chown -R nginx:nginx /run/nginx /var/lib/nginx /var/log/nginx
RUN rc-update add nginx default
RUN echo $'proxy_set_header Host $http_host;\n\
proxy_set_header X-Real-IP $remote_addr;\n\
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;\n\
proxy_set_header X-Forwarded-Proto $scheme;\n' > /etc/nginx/proxy_params
