FROM openjdk:11.0.3-jdk

ENV repo_name management_backend
ENV repo_link https://github.com/elastcbots/${repo_name}
ENV JAR_VERSION 1.0

ARG DATASOURCE_URL
ARG DATASOURCE_USERNAME
ARG DATASOURCE_PASSWORD

ENV ELB__DATASOURCE_URL=$DATASOURCE_URL
ENV ELB__DATASOURCE_USERNAME=$DATASOURCE_USERNAME
ENV ELB__DATASOURCE_PASSSWORD=$DATASOURCE_PASSWORD

ADD . $ELB__DATASOURCE_URL
ADD . $ELB__DATASOURCE_USERNAME
ADD . $ELB__DATASOURCE_PASSWORD

RUN apt-get update
RUN apt-get install -y git
RUN apt-get install -y maven

# RUN git clone ${repo_link}
RUN git clone https://github.com/elasticbots/management_backend
WORKDIR ${repo_name}

RUN mvn package

EXPOSE 9093
CMD java -jar target/${repo_name}-${JAR_VERSION}-SNAPSHOT.jar
