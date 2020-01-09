FROM certbot/certbot:v0.27.1

RUN wget https://bitbucket.org/schulebruegg/docker-certbot-inwx/get/master.zip && \
    unzip master.zip && \
    pip install ./*-docker-certbot-inwx-* dnspython && \
    rm -rf certbot-dns-inwx-master master.zip
