FROM ubuntu:18.04
LABEL maintainer="kosar@freedom.valor.ua"
LABEL vendor="1node"
LABEL created="10-02-2019"
LABEL lastUpdate="21-03-2019"
LABEL description="nginx container based on UBUNTU 18.04"
EXPOSE 80 443
ENV DEBIAN_FRONTEND noninteractive
RUN apt update && apt upgrade -y
# set timezone
RUN echo 'Europe/Kiev' > /etc/timezone
RUN apt install -y tzdata gnupg curl ca-certificates gnupg2
# install nginx
RUN curl -fsSL https://nginx.org/keys/nginx_signing.key | apt-key add - \
    && echo "deb http://nginx.org/packages/mainline/ubuntu bionic nginx" \
    | tee /etc/apt/sources.list.d/nginx.list \
    && apt update
RUN apt install -y nginx-full
CMD ["nginx", "-g", "daemon off;"]
