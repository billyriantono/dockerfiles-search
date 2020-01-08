FROM node:alpine

RUN apk add --update ncurses bash bash-doc bash-completion tmux

RUN npm install --global \
    # Node Tools
    @adonisjs/cli create-noderize n nodemon \
    # Front-End Tools
    create-react-app gatsby-cli \
    vue-cli \
    # Language Tools
    coffeescript \
    typescript ts-node

COPY scripts/* /home/node/bin/
COPY dotfiles/* /home/node/

RUN mkdir /workspace &&\
    chown -R node:node /workspace &&\
    chown -R node:node /home/node &&\
    chmod -R +x /home/node/bin

USER node
WORKDIR /workspace
ENV PATH=$PATH:/home/node/bin
EXPOSE 1000-10000
CMD ["bash"]
