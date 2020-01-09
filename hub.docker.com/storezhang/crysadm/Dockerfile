FROM storezhang/alpine

MAINTAINER storezhang "storezhang@gmail.com"
LABEL architecture="AMD64/x86_64" version="latest" build="2018-12-25"

EXPOSE 22000

ENV CRYSADM_DIR /opt/thunder/crysadm
ADD ./conf/docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh
ADD ./conf/redis.conf /redis/conf/redis.conf

# 开始打包
RUN set -ex \
    \
    && apk update \
    && apk --no-cache add su-exec python3 python3-dev redis \
    && pip3 install --upgrade pip \
    && pip3 install redis \
        requests \
        flask \
    # 修复Redism内存
    && echo "vm.overcommit_memory=1" > /etc/sysctl.conf \
    && adduser -S crysadm \
    && mkdir -p ${CRYSADM_DIR} \
    && mkdir /data \
    && chown -R crysadm "${CRYSADM_DIR}" \
    && chown -R crysadm /data \
    && chmod +x /usr/local/bin/docker-entrypoint.sh \
    && rm -rf /var/cache/apk/*

COPY ./ ${CRYSADM_DIR}

# Redis数据库保存目录
VOLUME ["/data"]

# 运行服务
ENTRYPOINT ["su-exec", "crysadm", "/usr/local/bin/docker-entrypoint.sh"]
