FROM quay.io/ansible/molecule

RUN addgroup -g 1000 jenkins \
  && adduser \
    -h /home/jenkins \
    -u 1000 \
    -G jenkins \
    -s /bin/sh \
    -D jenkins \
  && echo jenkins:jenkins | chpasswd

USER jenkins

WORKDIR /ansible
