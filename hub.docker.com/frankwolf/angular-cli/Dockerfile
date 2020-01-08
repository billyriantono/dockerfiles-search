FROM node:6
MAINTAINER "Frank Wolf <FrankWolf@gmx.de>"
LABEL Maintainer="Frank Wolf <FrankWolf@gmx.de>" \
      Name="angular-cli" \
      Version=1.4.9

EXPOSE 4200

RUN npm install -g @angular/cli \
      && npm cache clean \
      && ng completion --bash >> /home/node/.bashrc

# image node:6 has user 'node' with id 1000
USER node

VOLUME /data
WORKDIR /data

CMD ["/bin/bash"]
ENTRYPOINT []
