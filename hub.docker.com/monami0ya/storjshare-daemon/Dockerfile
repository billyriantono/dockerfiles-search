FROM node:6.9.5
MAINTAINER Masaki Muranaka <monaka@monami-ya.com>
 
RUN useradd --user-group --create-home --shell /bin/false app
RUN npm install --global storjshare-daemon
 
ENV HOME=/home/app
USER app
WORKDIR /home/app
RUN mkdir -p .config/storjshare storage_root
VOLUME /home/app/.config/storjshare
VOLUME /home/app/storage_root

ENTRYPOINT [ "storjshare" ]
CMD [ "help" ]
