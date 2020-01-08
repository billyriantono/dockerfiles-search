FROM nginx:1.13-alpine

RUN mkdir -p /etc/ssl/certs /nsqbin 

COPY data/* /nsqbin/

RUN chmod -R +x /nsqbin/

WORKDIR /nsqbin

EXPOSE 4150 4151 4152 4160 4161
