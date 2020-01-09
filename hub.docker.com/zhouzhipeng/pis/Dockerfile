FROM zhouzhipeng/git as GitEnv

RUN  git clone https://github.com/zhouzhipeng/pis.git .

#RUN echo "test zhou $(ls -a /git)"

FROM maven:3.5.2-alpine as BuildEnv

ENV MY_HOME=/usr/src/app
RUN mkdir -p $MY_HOME
WORKDIR $MY_HOME

# add source
COPY --from=GitEnv /git /usr/src/app

# run maven package
RUN mvn clean package -Dmaven.test.skip=true


FROM tomcat:8-jre8-alpine

RUN rm -rf /usr/local/tomcat/webapps/*

COPY --from=BuildEnv /usr/src/app/target/pis-1.0.0.war /usr/local/tomcat/webapps/ROOT.war

