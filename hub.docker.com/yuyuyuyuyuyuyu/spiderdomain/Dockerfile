FROM carsharing/alpine-oraclejdk8-bash

EXPOSE 8038

VOLUME /tmp

RUN mkdir /root/.m2
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo 'Asia/Shanghai' >/etc/timezoneg

COPY . /root/spider
WORKDIR /root/spider

RUN ./mvnw package && ./mvnw install

CMD ./mvnw spring-boot:run
