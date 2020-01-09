FROM alpine
MAINTAINER carcassi@umich.edu

ENV CONFIGURATION_PARAMETER_1=defaultValue1 \
    CONFIGURATION_PARAMETER_2=defaultValue2

COPY entrypoint.sh /sbin/entrypoint.sh
COPY example.conf /etc/example/example.conf

RUN mkdir -p /var/example/data && \
    mkdir -p /var/example/scratch

ENTRYPOINT ["/sbin/entrypoint.sh"]
