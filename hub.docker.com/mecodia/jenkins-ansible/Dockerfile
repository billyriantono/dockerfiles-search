FROM jenkins/jnlp-slave:alpine
MAINTAINER mecodia GmbH

USER root
RUN apk update && apk add python3 py3-cffi py3-pynacl py3-paramiko py3-crypto
RUN pip3 install --no-cache-dir ansible
USER jenkins
