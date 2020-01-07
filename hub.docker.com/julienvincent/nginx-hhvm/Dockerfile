# julienvincent/nginx-hhvm:3.10.1

FROM julienvincent/nginx:1.9.2
MAINTAINER Julien Vincent "julienlucvincent@gmail.com"

ENV HHVM_VERSION 3.10.1~jessie

# Install HHVM
RUN apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0x5a16e7281be7a449
RUN echo deb http://dl.hhvm.com/debian jessie main | tee /etc/apt/sources.list.d/hhvm.list

RUN apt-get clean && \
    apt-get update && \
    apt-get install -y hhvm && \
    apt-get clean -y && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Update Config
COPY container/default.conf /etc/nginx/conf.d/default.conf
COPY container/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

VOLUME ["/etc/nginx/conf.d", "/data/www"]

CMD ["/usr/bin/supervisord"]
EXPOSE 80 443