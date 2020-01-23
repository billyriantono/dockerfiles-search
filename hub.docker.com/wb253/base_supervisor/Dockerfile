FROM alpine
MAINTAINER wangbin <wangbin253@gmail.com>

RUN    echo 'http://mirrors.ustc.edu.cn/alpine/edge/main' > /etc/apk/repositories && \
    echo 'http://mirrors.ustc.edu.cn/alpine/edge/community' >> /etc/apk/repositories && \
    echo 'http://mirrors.ustc.edu.cn/alpine/edge/testing' >> /etc/apk/repositories && \

    apk --update add \
        --repository http://mirrors.ustc.edu.cn/alpine/edge/main \
        --repository http://mirrors.ustc.edu.cn/alpine/edge/community \
        pcre \
        supervisor && \
        mkdir -p /etc/supervisor/conf.d \
                 /var/log/supervisor
        
ADD ./supervisord.conf /etc/supervisor/supervisord.conf

CMD ["supervisord", "-c", "/etc/supervisor/supervisord.conf"]
