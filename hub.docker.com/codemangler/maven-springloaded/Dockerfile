FROM maven:3.5.4-jdk-8-alpine
MAINTAINER CodeMangler <hsdpal@gmail.com>

VOLUME /tmp
WORKDIR /tmp
COPY . /tmp
RUN mvn dependency:resolve

CMD ["mvn"]
