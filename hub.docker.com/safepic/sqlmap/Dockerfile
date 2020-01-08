FROM alpine
LABEL maintainer "contact@ilyaglotov.com"
ARG version=1.3.11

RUN apk update \
  && apk add --no-cache python git \
  && git clone --depth=1 \
               --single-branch --branch=${version} \
               https://github.com/sqlmapproject/sqlmap.git \
               /root/sqlmap \
  && apk del git \
  && rm -rf /root/sqlmap/.git \
  && rm -rf /var/cache/apk/* 
  
WORKDIR /root/sqlmap
ENTRYPOINT ["python", "sqlmap.py"]
