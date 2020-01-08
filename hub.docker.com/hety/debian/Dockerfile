FROM debian
RUN apt update && apt install -y apt-transport-https && rm -rf /var/lib/apt/lists/* && apt clean && sed -i 's/deb.debian.org/mirrors.cloud.tencent.com/' /etc/apt/sources.list && sed -i 's/security.debian.org/mirrors.cloud.tencent.com/' /etc/apt/sources.list && sed -i 's/http:/https:/' /etc/apt/sources.list
