FROM serafinlabs/nodejs:10
LABEL maintainer="Nicolas Degardin <degardin.n@gmail.com>"

USER root
RUN apk --update --no-cache add nodejs-doc nodejs-dev
RUN /opt/docker/install-devtools.sh && rm /opt/docker/install-devtools.sh
RUN sed -ri 's#^plugins=\(([^)]+)\)$#plugins=(\1 node npm gulp bower)#g' /etc/zsh/zshrc
ADD files/ssh_config /etc/ssh_config
RUN chmod 400 /etc/ssh_config
RUN mkdir -p /home/node/.npm/lib/node_modules
RUN mkdir -p /home/node/.npm/bin
RUN chmod -R a+rw /home/node/.npm/lib/node_modules
RUN chmod -R a+rw /home/node/.npm

USER node
RUN npm install --global typescript bunyan depcheck
RUN echo '' > $HOME/.zshrc
RUN mkdir -p /home/node/cache && touch /home/node/cache/npm_completion
ENV ZSH_CACHE_DIR /home/node/cache
ENV PATH="/home/node/.npm/bin:$PATH"

EXPOSE 80
EXPOSE 9229

ADD files/startup.sh /opt/docker/startup.sh
ADD files/build.sh /opt/docker/build.sh

VOLUME ["/home/node/.ssh"]
VOLUME ["/srv"]

ENTRYPOINT ["/opt/docker/startup.sh"]
CMD ["npm", "start"]