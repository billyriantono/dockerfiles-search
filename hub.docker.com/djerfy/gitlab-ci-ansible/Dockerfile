FROM alpine:3.11
LABEL description="Ansible on Alpine 3.11 and Python 3.7" \
      maintainer="Djerfy <djerfy@gmail.com>"

RUN apk -U add gcc make python3 python3-dev openssl-dev && \
    apk -U add py3-cffi py3-bcrypt py3-cryptography py3-pynacl && \
    pip3 install --upgrade pip && \
    pip3 install ansible==2.9.3

CMD ["ansible", "--version"]

