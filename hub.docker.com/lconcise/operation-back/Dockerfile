FROM anapsix/alpine-java:8_server-jre_unlimited

ADD ./pil/ /mnt/

RUN echo "http://mirrors.ustc.edu.cn/alpine/v3.4/main" > /etc/apk/repositories \
 && echo "http://mirrors.ustc.edu.cn/alpine/v3.4/community" >> /etc/apk/repositories \
 && apk update \
 && apk add tzdata \
 && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
 && echo "Asia/Shanghai" >  /etc/timezone \
 && apk del tzdata \
 && rm -rf /var/cache/apk/* \
 && apk add --no-cache musl-dev python3-dev gcc python3 zlib-dev jpeg-dev freetype-dev lcms2-dev openjpeg-dev tiff-dev tk-dev tcl-dev && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade /mnt/pip-19.2.3-py2.py3-none-any.whl && \
    pip3 install --upgrade /mnt/setuptools-41.2.0-py2.py3-none-any.whl && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
    if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \
    pip install /mnt/Pillow-6.0.0.tar.gz && \
    rm -r /root/.cache