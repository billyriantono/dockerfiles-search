FROM maven
EXPOSE 8004
RUN mvn --version
RUN mkdir ~/workdir
RUN git clone https://github.com/rsridivya/simple_http_server.git
RUN mv simple_http_server /opt
WORKDIR /opt/simple_http_server
RUN pwd
RUN ls
RUN mvn install
RUN echo "java -cp /opt/simple_http_server/target/simple_http_server-0.0.1-SNAPSHOT.jar pkg.gannet.simple_http_server.SimpleHTTPServer" > /opt/hello
RUN chmod +x /opt/hello
