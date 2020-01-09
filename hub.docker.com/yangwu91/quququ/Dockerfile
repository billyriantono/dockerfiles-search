FROM rastasheep/ubuntu-sshd:18.04
MAINTAINER yangwu91 yangwu91@outlook.com

EXPOSE 443
EXPOSE 80
EXPOSE 2222

COPY . /ssr-docker-source/

RUN export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get install -y python \
                       libsodium23 libnet1-dev libpcap0.8-dev \
                       build-essential \
                       curl \
                       openssh-server \
                       git \
                       ntpdate \
                       nginx \
                       vim \
					   iputils-ping \
					   net-tools &&\

# SSR server
    mkdir -p /opt && \
    cp -r /ssr-docker-source/ssr-custom /opt/ssr-custom && \
    cp /ssr-docker-source/user-config.json /opt/ssr-custom/user-config.json && \
    find /opt/ssr-custom/ -name "*.sh" -type f | xargs -I {} chmod +x {} && \
    mkdir -p /var/log/ && \
    touch /var/log/shadowsocksr.log && \

# SSH
    echo 'root:EEXe9vOKsbBC7aKl' |chpasswd && \
    mkdir -p /var/run/sshd && \
    mkdir -p /ssh && \
    chmod 700 /ssh && \
	cp /ssr-docker-source/authorized_keys /ssh &&  \
    sed -ri \
        -e 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' \
        -e 's/UsePAM yes/#UsePAM yes/g' \
        -e 's/^#Port 22/Port 2222/g' \
        -e 's/#PasswordAuthentication yes/PasswordAuthentication no/g' \
        -e 's;^#AuthorizedKeysFile.+$;AuthorizedKeysFile /ssh/authorized_keys;g' \
        /etc/ssh/sshd_config && \
# v2ray
    wget https://install.direct/go.sh && \
    bash go.sh && \
    rm -f go.sh && \
    cp /ssr-docker-source/v2ray.config.json /etc/v2ray/config.json && \
    cp /ssr-docker-source/5GmUQzbYOZ.yahoo.co.jp_cert.pem /etc/v2ray/5GmUQzbYOZ.yahoo.co.jp_cert.pem && \
    cp /ssr-docker-source/5GmUQzbYOZ.yahoo.co.jp_key.pem /etc/v2ray/5GmUQzbYOZ.yahoo.co.jp_key.pem && \

# time zone
#   ln -snf /usr/share/zoneinfo/America/New_York /etc/localtime && \
#	echo "America/New_York" > /etc/timezone && \

# nginx
    rm -f /etc/nginx/sites-enabled/default && \
    cp /ssr-docker-source/nginx.default.cfg /etc/nginx/sites-enabled/ && \
    rm -f /var/www/html/index.nginx-debian.html && \
    cp /ssr-docker-source/index.html /var/www/html/ && \


# Miscellaneous
    cp /ssr-docker-source/VERSION /opt/ && \

# Init
    cp /ssr-docker-source/init.sh /opt/init.sh && \
    chmod +x /opt/init.sh
WORKDIR /

ENTRYPOINT ["/opt/init.sh"]
