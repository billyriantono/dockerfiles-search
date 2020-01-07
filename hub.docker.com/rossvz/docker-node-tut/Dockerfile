FROM node:4.3.2
RUN npm install --global npm@3.8.1

ENV HOME=/home/app

COPY package.json npm-shrinkwrap.json $HOME/chat/
#RUN chown -R app:app $HOME/

#USER app
WORKDIR $HOME/chat
RUN npm install

#USER root
COPY . $HOME/chat

CMD ["node","index.js"]