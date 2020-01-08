FROM node

RUN useradd -ms /bin/bash hubot

RUN npm install -g coffee-script yo generator-hubot

COPY ./docker-entrypoint.sh /

USER hubot
ENV HOME /home/hubot
WORKDIR /home/hubot

VOLUME /home/hubot

EXPOSE 80

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["shell"]
