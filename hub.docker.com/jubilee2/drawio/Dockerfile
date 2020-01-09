FROM frekele/ant:1.10.3-jdk8 as BUILD
RUN apt-get update && apt-get install git -y && cd /usr && git clone -b v10.7.7 --depth=1 https://github.com/jgraph/drawio.git build && cd build/etc/build/ && ant war

FROM tomcat:9.0 as TARGET
COPY --from=BUILD /usr/build/build/draw.war /usr/local/tomcat/webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
