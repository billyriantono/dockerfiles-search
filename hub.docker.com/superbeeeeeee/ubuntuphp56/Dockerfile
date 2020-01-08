# build image : docker build -t "test:latest" .
# setup container : docker run -it --privileged --name fb test
# exec bash : docker exec -it fb /bin/bash
FROM ubuntu:16.04
LABEL maintainer="cboudereau"

COPY docker-entrypoint.sh /usr/local/bin

RUN apt-get update -y && apt-get install -y \
software-properties-common \
dialog \
whois \
sudo \
&& LC_ALL=C.UTF-8 sudo add-apt-repository -y ppa:ondrej/php \
&& export DEBIAN_FRONTEND=noninteractive DEBCONF_NONINTERACTIVE_SEEN=true \
&& sudo echo "Etc/UTC" > /etc/timezone \
&& sudo apt-get update -y && sudo apt-get install -y \
git \
php5.6

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]
CMD ["init"]