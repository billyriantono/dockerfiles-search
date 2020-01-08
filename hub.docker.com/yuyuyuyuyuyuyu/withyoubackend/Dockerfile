FROM carsharing/alpine-oraclejdk8-bash
MAINTAINER yuyuyuyuyuyuyu

EXPOSE 8018

VOLUME /tmp

RUN mkdir /root/.m2
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' >/etc/timezone

COPY . /root/withyou
WORKDIR /root/withyou

RUN ./mvnw package && ./mvnw install

CMD ./mvnw spring-boot:run
