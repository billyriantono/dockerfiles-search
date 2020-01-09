FROM alpine:latest

COPY ./ /srv

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories \
    && apk update \
    && apk add python2 \
    && python -m ensurepip \
    && pip install \
        tornado \
        futures \
    && find / -name "*.pyc" | xargs rm -f \
    && rm -f /var/cache/apk/*
CMD ["python", "/srv/app.py"]