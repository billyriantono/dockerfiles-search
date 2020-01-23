FROM debian:buster AS build

ENV DEBIAN_FRONTEND noninteractive

RUN \
sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
sed -i "s#deb.debian.org#mirrors.aliyun.com#g" /etc/apt/sources.list && \
sed -i "s#security.debian.org#mirrors.aliyun.com#g" /etc/apt/sources.list && \
apt-get clean && \
apt-get update && \
apt-get install build-essential openssl libssl-dev curl vim ca-certificates -y -q


RUN curl -sSL -O https://raw.githubusercontent.com/vanhauser-thc/THC-Archive/master/Tools/amap-5.4.tar.gz

RUN tar -xvf amap-5.4.tar.gz
WORKDIR /amap-5.4
RUN sed "s/^LIBDIRS=.*/LIBDIRS=\`cat \/etc\/ld.so.conf.d\/*.conf 2> \/dev\/null\`/g" -i ./configure
RUN ./configure --prefix=/
RUN make && make install

FROM debian:buster

LABEL version="2.3.1" \
      author="Author 7error (https://github.com/7error)" \
      docker_build="docker build -t 7error/kkkbox:2 ." \
      docker_run_basic="docker run --rm 7error/kkkbox:2 /bin/sh -c 'ping -c1 8.8.8.8'" \
      docker_run_advanced="docker run --rm 7error/kkkbox:2 /bin/sh -c 'nping -c2 8.8.8.8'"

ENV RG_VERSION=11.0.2
ENV VEGETA_VERSION=12.7.0
ENV SOPS_VERSION=3.5.0
ENV DEBIAN_FRONTEND noninteractive
ENV TZ=Asia/Shanghai

RUN \
sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
sed -i "s#deb.debian.org#mirrors.aliyun.com#g" /etc/apt/sources.list && \
sed -i "s#security.debian.org#mirrors.aliyun.com#g" /etc/apt/sources.list && \
apt-get clean && \
apt-get update && \
apt-get -y upgrade && \
apt-get install --no-install-recommends -y -q \
fping curl wget netcat nmap jq dnsutils iproute2 ncat iputils-ping mtr-tiny \
socat traceroute htop net-tools iptables nload vnstat tcpdump openssl strace \
openssh-client procps \
aria2 tree lrzsz rsync knot-dnsutils \
hping3 psmisc dmitry whois \
ncaptool packit sendip ngrep libndpi-bin \
pwgen zip unzip \
ca-certificates \
&& rm -rf /var/lib/apt/lists/*


COPY --from=build /bin/amapcrap /bin/amapcrap
COPY --from=build /bin/amap /bin/amap
COPY --from=build /etc/appdefs* /etc/


RUN set -x \
&& curl -sSL -O -k https://github.com/BurntSushi/ripgrep/releases/download/${RG_VERSION}/ripgrep-${RG_VERSION}-x86_64-unknown-linux-musl.tar.gz \
&& tar xzf ripgrep-${RG_VERSION}-x86_64-unknown-linux-musl.tar.gz \
&& mv ripgrep-${RG_VERSION}-x86_64-unknown-linux-musl/rg /usr/bin/ \
&& rm -rf ripgrep-${RG_VERSION}-x86_64-unknown-linux-musl.tar.gz \
&& rm -rf ripgrep-${RG_VERSION}-x86_64-unknown-linux-musl

RUN set -x \
&& curl -sSL -o /tmp/vegeta.tar.gz -k https://github.com/tsenart/vegeta/releases/download/v${VEGETA_VERSION}/vegeta-${VEGETA_VERSION}-linux-amd64.tar.gz \
&& tar xzf /tmp/vegeta.tar.gz -C /usr/bin/ \
&& rm /tmp/vegeta.tar.gz


RUN set -x \
&& curl -sSLk -o /usr/bin/sops https://github.com/mozilla/sops/releases/download/v${SOPS_VERSION}/sops-v${SOPS_VERSION}.linux \
&& chmod +x /usr/bin/sops

RUN set -x \
&& curl -sSL -o /tmp/docker.tgz -k https://download.docker.com/linux/static/stable/x86_64/docker-19.03.5.tgz \
&& tar xvf /tmp/docker.tgz -C /tmp \
&& cp /tmp/docker/docker /usr/bin/ \
&& rm /tmp/docker.tgz \
&& rm -rf /tmp/docker

RUN ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && dpkg-reconfigure --frontend noninteractive tzdata

ENTRYPOINT []

