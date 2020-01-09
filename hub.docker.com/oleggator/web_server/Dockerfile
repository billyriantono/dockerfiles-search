FROM debian:stretch-slim AS build

RUN apt-get update && apt-get -y install cmake g++ qtbase5-dev

ADD . /root
WORKDIR /root

RUN cmake -DCMAKE_BUILD_TYPE=Release . && cmake --build .

RUN cp /root/web_server /bin/web_server
RUN cp /root/httpd.conf /etc/

EXPOSE 80
ENTRYPOINT ["/bin/web_server"]
