FROM lighthero/jdk-chrome:8

ADD ./project /project
WORKDIR /project

RUN mvn clean dependency:resolve dependency:resolve-plugins 
RUN rm -rf /project
