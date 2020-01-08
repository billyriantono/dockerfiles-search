FROM ubuntu:latest
RUN \
apt update && \
apt -y upgrade && \
apt -y install nano wget && \
cd /opt && \
VERSION=2.0.19 && \
wget https://github.com/jedisct1/dnscrypt-proxy/releases/download/$VERSION/dnscrypt-proxy-linux_x86_64-$VERSION.tar.gz && \
tar xvf dnscrypt-proxy-linux_x86_64-$VERSION.tar.gz && \
rm dnscrypt-proxy-linux_x86_64-$VERSION.tar.gz && \
mv linux-x86_64 dnscrypt-proxy && \
cd /opt/dnscrypt-proxy && \
cp example-dnscrypt-proxy.toml dnscrypt-proxy.toml && \
sed -i -e "s/\, '\[::1\]:53'//g" dnscrypt-proxy.toml && \
apt clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
exit 0
WORKDIR /opt/dnscrypt-proxy
ENTRYPOINT ["./dnscrypt-proxy"]
