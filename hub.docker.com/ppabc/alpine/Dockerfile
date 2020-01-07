FROM alpine:3.7
LABEL maintainer="ppabc (ppabc@qq.com)"

### Add Zabbix User First
    RUN set -x ; \
        addgroup -g 10050 zabbix ; \
        adduser -S -D -H -h /dev/null -s /sbin/nologin -G zabbix -u 10050 zabbix ;\
        
### Add Core Utils
       apk --no-cache upgrade ; \
       apk --no-cache add \
            bash \
            curl \
            grep \
            less \
            sudo \
            tzdata \
            ; \
       rm -rf /var/cache/apk/* ; \
       rm -rf /etc/logrotate.d/acpid ; \
       cp -R /usr/share/zoneinfo/Asia/Shanghai /etc/localtime ; \
       echo 'Asia/Shanghai' > /etc/timezone ; \
       echo '%zabbix ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers ; \

