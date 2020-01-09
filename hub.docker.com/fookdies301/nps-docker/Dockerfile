FROM alpine:edge
LABEL maintainer="Fangkun Peng <pengfkun@gmail.com>"
ENV Bridge_type tcp
ENV Http_port 6680
ENV Https_port 6681
ENV Bridge_port 6682
ENV Web_port 6683
ARG Public_vkey
ENV Public_vkey=${Public_vkey}
ARG Host
ENV Host=${Host}
ENV UserName admin
ENV Passwd 123
ARG Auth_Key
ENV Auth_Key=${Auth_Key}
ARG Auth_Crypt_Key
ENV Auth_Crypt_Key=${Auth_Crypt_Key}

ARG CN_MIRROR=false
RUN if [ "$CN_MIRROR" = true ]; then sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories; fi

RUN set -ex \
   && apk add --no-cache bash \
   && apk add --no-cache --virtual TMP curl \
   && file_url=$(curl -s 'https://api.github.com/repos/cnlh/nps/releases/latest' | grep "browser_download_url.*linux_amd64_server.tar.gz" | cut -d '"' -f 4) \
   && curl -sL "$file_url" | tar -xzv -C /tmp \
   && mkdir -p /etc/nps \
   && cp -r /tmp/nps/conf /etc/nps/ \
   && cp -r /tmp/nps/web /etc/nps/ \
   && cp /tmp/nps/nps /usr/bin/ \
   && mkdir /nps \
   && apk del TMP \
   && rm -rf /var/cache/apk/* \
   && rm -rf /tmp/*

ENV PATH /etc/nps:$PATH
COPY nps.conf /etc/nps/conf/nps.conf
COPY entrypoint.sh /usr/bin/
EXPOSE ${Http_port} ${Https_port} ${Bridge_port} ${Web_port}
RUN chmod +x /usr/bin/entrypoint.sh

WORKDIR /nps

ENTRYPOINT ["/usr/bin/entrypoint.sh"]
CMD ["/usr/bin/nps"]
