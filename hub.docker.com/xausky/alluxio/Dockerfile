FROM java:7

MAINTAINER xausky xausky@gmail.com

ENV ALLUXIO_VERSION 1.2.0

COPY init.sh /usr/local/bin/

COPY entrypoint.sh /usr/local/bin/

RUN /usr/local/bin/init.sh

ENTRYPOINT ["entrypoint.sh"]

EXPOSE 22 19999 30000

CMD ["bash"]
