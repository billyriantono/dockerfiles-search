FROM docker:stable
# 111
RUN apk add --no-cache openssh py2-pip curl git gcc python2-dev musl-dev libffi-dev openssl-dev make && \ 
  pip install --upgrade pip && \
  pip install docker-compose && \
  rm -rf /var/cache/apk/*
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s \
    https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && \
    chmod +x ./kubectl && mv ./kubectl /usr/local/bin/kubectl

CMD ["kubectl","version"]
