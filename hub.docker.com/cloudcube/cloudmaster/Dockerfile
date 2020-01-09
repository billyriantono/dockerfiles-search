FROM cloudcube/nodejs

MAINTAINER DavidZhao <zhaohaibin@outlook.com>

ENV REFRESHED_AT 2015-12-12 23:44

WORKDIR /root

ADD auth/id_rsa_docker /root/.ssh/id_rsa

ADD auth/id_rsa_docker.pub /root/.ssh/id_rsa.pub

ADD conf.d/config /root/.ssh/config

RUN chmod 0600 /root/.ssh/*

ADD conf.d/cloudmaster.conf /etc/supervisor/conf.d/cloudmaster.conf

RUN git clone github:haibinpark/cloudmaster.git /app/cloudmaster

WORKDIR /app/cloudmaster

RUN git fetch && git checkout -b develop origin/develop

RUN npm install

CMD ["/nodeserver/startup"]
