FROM almir/webhook

RUN  apk --update --upgrade add docker curl bash python && \
     curl -L -o /tmp/get-pip.py https://bootstrap.pypa.io/get-pip.py && \
     python /tmp/get-pip.py && \
     pip install docker-compose && \
     rm -f /tmp/get-pip.py && \
     rm -rf /var/cache/apk/* 