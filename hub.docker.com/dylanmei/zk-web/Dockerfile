# dylanmei/zk-web
FROM debian:jessie

RUN apt-get update && apt-get install -y --no-install-recommends wget git openjdk-7-jdk
ADD https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein /bin/lein
RUN chmod 755 /bin/lein
ENV LEIN_ROOT=yes
RUN lein

#RUN git clone https://github.com/qiuxiafei/zk-web.git
ADD . /zk-web
WORKDIR /zk-web
RUN lein jar

ENV DEFAULT_NODE ""
ENV PORT         8080
EXPOSE 8080

CMD lein run
