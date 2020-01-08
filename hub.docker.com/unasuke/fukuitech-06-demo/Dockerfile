FROM unasuke/h2o-alpine:latest

WORKDIR /etc/h2o

COPY h2o.conf /etc/h2o/h2o.conf
COPY index.html /etc/h2o/index.html

EXPOSE 3000

CMD ["/usr/local/bin/h2o", "-m", "master", "-c", "h2o.conf"]
