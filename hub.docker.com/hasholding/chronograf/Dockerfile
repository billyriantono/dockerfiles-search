FROM hasholding/alpine-base

LABEL maintainer "Levent SAGIROGLU <LSagiroglu@gmail.com>"

ARG VERSION=1.4.2.3
ENV BOLT_PATH /shared/chronograf-v1-.db
VOLUME /shared
WORKDIR /tmp
RUN apk add --no-cache wget 
RUN wget https://dl.influxdata.com/chronograf/releases/chronograf-${VERSION}-static_linux_amd64.tar.gz -O chronograf.tar.gz
RUN tar xvfz chronograf.tar.gz  -C /bin  --strip 2
RUN rm -r *
EXPOSE 8888
ENTRYPOINT ["/bin/chronograf"]
