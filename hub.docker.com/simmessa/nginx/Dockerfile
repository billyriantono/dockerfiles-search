# Experimental Docker image made with nginx 1.15.2 + PageSpeedMod 1.13.35 beta 2
# date: 2018-08-06
# https://hub.docker.com/r/simmessa/nginx/

FROM debian:stretch-slim
MAINTAINER simmessa@gmail.com

ENV DEPS curl build-essential zlib1g-dev libpcre3 libpcre3-dev unzip uuid-dev wget libssl1.0-dev libgd-dev libgeoip-dev
# Apt and deps
RUN apt-get -qq update && apt-get install -yqq $DEPS 
#nginx

# build nginx and pagespeedmod, the official PageSpeedMod build script had to be modified, and copied to our container
COPY psbuild.bash /tmp/psbuild.bash
RUN bash /tmp/psbuild.bash

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
&& ln -sf /dev/stderr /var/log/nginx/error.log

#expose nginx
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
