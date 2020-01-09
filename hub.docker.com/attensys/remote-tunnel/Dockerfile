FROM buildo/alpine-ssh

WORKDIR /usr/src/app

ENV REMOTE_HOST 18.195.122.238
ENV REMOTE_USER ec2-user
ENV CERTIFICATE_PATH attensys.pem

COPY attensys.pem .
RUN chmod 400 attensys.pem

COPY tunnel.sh .

CMD [ "/bin/sh", "tunnel.sh"]