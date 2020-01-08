FROM ubuntu:14.04

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update && \
    apt-get install -yq --no-install-recommends wget curl rsync && \
    wget --no-check-certificate --content-disposition "https://packages.chef.io/files/stable/chef-server/12.17.33/ubuntu/14.04/chef-server-core_12.17.33-1_amd64.deb" && \
    dpkg -i chef-server*.deb && \
    rm chef-server*.deb && \
    rm -rf /var/lib/apt/lists/*

COPY run.sh configure_chef.sh /usr/local/bin/

VOLUME /var/log

EXPOSE 443 80

CMD ["run.sh"]
