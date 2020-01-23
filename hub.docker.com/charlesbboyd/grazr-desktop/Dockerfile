FROM node:8
LABEL maintainer="Charles <charles@charlesboyd.me>"

RUN apt-get update
RUN apt-get install -y git build-essential sudo vim nano
RUN sudo npm install --unsafe-perm -g @angular/cli@1.6.8

WORKDIR /grazr/src/grazr-desktop
EXPOSE 4200

COPY containerboot.sh /grazr/
COPY serveboot.sh /grazr/
RUN chmod ugo+rx /grazr/serveboot.sh

CMD ["/grazr/containerboot.sh"]
