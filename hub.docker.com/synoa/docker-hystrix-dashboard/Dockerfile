FROM openjdk:8-jre-alpine
MAINTAINER Oliver Koch <o.koch@synoa.de>

ENV JETTY_VERSION=9.4.6.v20170531
ENV HYSTRIX_DASHBOARD_VERSION=1.5.9

ADD https://repo1.maven.org/maven2/org/eclipse/jetty/jetty-runner/${JETTY_VERSION}/jetty-runner-${JETTY_VERSION}.jar /jetty-runner.jar
ADD https://repo1.maven.org/maven2/com/netflix/hystrix/hystrix-dashboard/${HYSTRIX_DASHBOARD_VERSION}/hystrix-dashboard-${HYSTRIX_DASHBOARD_VERSION}.war /hystrix-dashboard.war

EXPOSE 9090

CMD [ "java", "-jar", "/jetty-runner.jar", "--port", "9090", "/hystrix-dashboard.war" ]
