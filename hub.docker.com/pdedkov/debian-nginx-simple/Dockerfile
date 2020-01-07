FROM debian:latest
MAINTAINER Pavel E. Dedkov <pavel.dedkov@gmail.com>

# env
ENV TIMEZONE Europe/Moscow

# install required software
RUN apt-get update \ 
&& apt-get upgrade -y \
&& apt-get install -y --no-install-recommends nginx\
&& apt-get autoclean \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# configure nginx
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

EXPOSE 80

ENTRYPOINT ["nginx"]
