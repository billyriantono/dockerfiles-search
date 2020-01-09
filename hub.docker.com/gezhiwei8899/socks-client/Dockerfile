FROM debian:stretch-slim
RUN set -x \
    && apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y python-pip python-m2crypto wget\
    && pip install setuptools \
    && pip install shadowsocks \
    && sed -i '/EVP_CIPHER_CTX_cleanup/ {s/EVP_CIPHER_CTX_cleanup/EVP_CIPHER_CTX_reset/g;}' /usr/local/lib/python2.7/dist-packages/shadowsocks/crypto/openssl.py \
    && exit 0
EXPOSE 20800
CMD ["sslocal", "-c", "/etc/shadowsocks.json", "start"]
