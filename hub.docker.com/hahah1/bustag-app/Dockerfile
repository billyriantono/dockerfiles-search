FROM python:3.7-alpine

ENV TZ=Asia/Shanghai
ENV PYTHONPATH=/usr/lib/python3.7/site-packages/:$PYTHONPATH

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
    sed -i 's/dl-cdn.alpinelinux.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apk/repositories

WORKDIR /app

COPY requirements.txt .

RUN apk add --update --no-cache --virtual .build-deps g++ python-dev libxml2 && \
    apk add --no-cache libxslt-dev py3-numpy py3-pandas py3-scipy py3-scikit-learn bash && \
    easy_install pip && \
    pip install --no-cache-dir -r requirements.txt -i https://pypi.douban.com/simple && \
    sed -i '126d' /usr/local/lib/python3.7/site-packages/aspider/aspider.py && \
    apk del .build-deps

COPY bustag /app/bustag

RUN mkdir /app/docker

# ADD docker/crontab.txt /app/docker/crontab.txt

COPY docker/* /app/docker/

RUN touch /var/log/bustag.log

RUN chmod 755 /app/docker/*.sh

# RUN /usr/bin/crontab /app/docker/crontab.txt

EXPOSE 8000

LABEL maintainer="gxtrobot <gxtrobot@gmail.com>"

CMD ["/app/docker/entry.sh"]

