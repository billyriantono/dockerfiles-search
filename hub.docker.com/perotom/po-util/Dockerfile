FROM debian:9-slim
RUN apt-get update
RUN apt-get install -y sudo curl git gzip python gnupg2 software-properties-common build-essential libarchive-zip-perl
RUN /bin/bash -c "bash <(curl -sL https://particle.io/install-cli)"
RUN /bin/bash -c "bash <(curl -sL get.po-util.com)"
RUN po
