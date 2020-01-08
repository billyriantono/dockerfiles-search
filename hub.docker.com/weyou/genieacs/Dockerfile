FROM node
MAINTAINER Kelvin You <weyou.dev@gmail.com>

WORKDIR /app

RUN git clone https://github.com/genieacs/genieacs.git /app && \
    git checkout $(git tag -l v1.1.* --sort=-v:refname | head -n 1) && \
    npm install && npm run configure && npm run compile && \
	curl https://bootstrap.pypa.io/ez_setup.py -o - | python && \
	easy_install supervisor

ADD ./etc/supervisord.conf /etc/supervisord.conf
ADD ./config.json /app/config/config.json
ADD ./start.sh /app

CMD ["/bin/sh", "/app/start.sh"]
