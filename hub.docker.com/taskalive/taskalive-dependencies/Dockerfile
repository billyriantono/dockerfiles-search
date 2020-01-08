FROM alpine
# change source
RUN echo http://mirrors.ustc.edu.cn/alpine/latest-stable/main/ > /etc/apk/repositories && \
    echo http://mirrors.ustc.edu.cn/alpine/latest-stable/community/ >> /etc/apk/repositories && \
    apk --update --no-cache add alpine-sdk python3 python3-dev \
                                libffi libffi-dev libressl-dev jpeg-dev zlib-dev

# go into taskalive dir
WORKDIR /taskalive
ADD ./setup.py /taskalive
ADD ./README.md /taskalive
# update pip and install newest bson
RUN echo '[global]' >> /etc/pip.conf && \
    echo 'index-url = https://mirrors.ustc.edu.cn/pypi/web/simple' >> /etc/pip.conf && \
    echo 'format = columns' >> /etc/pip.conf && \
    echo 'no-cache-dir = false' >> /etc/pip.conf && \
    pip3 install cython && \
    python3 -m pip install -U pip  # update pip

RUN pip3 install -e . && \
    python3 setup.py clean --all && \
    pip3 uninstall -y taskalive && rm -r /taskalive && \
    apk del alpine-sdk libffi-dev libressl-dev python3-dev zlib-dev && \
    apk --update --no-cache add libressl
