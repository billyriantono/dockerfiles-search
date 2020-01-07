# Version: 0.0.1

FROM debian

MAINTAINER Yury Kavaliou <yury_kavaliou@epam.com>

ENV BS_SERVER /home/bsserver

RUN mkdir $BS_SERVER

COPY ./files/bs_server $BS_SERVER/bs_server
COPY ./files/bootstrap_server.ini $BS_SERVER/bootstrap_server.ini

WORKDIR $BS_SERVER

ENTRYPOINT ["./bs_server"]
CMD [""]

EXPOSE 5685/udp
