FROM alpine:latest

ENV UID=991 GID=991

RUN echo 'Setting up Repositories and installing Packages' \
	&& echo 'http://dl-cdn.alpinelinux.org/alpine/edge/community' >> /etc/apk/repositories \
	&& echo 'http://dl-cdn.alpinelinux.org/alpine/edge/main' >> /etc/apk/repositories \
	&& apk update \
    && apk add nodejs npm s6 go musl-dev ttyd \
	&& echo 'Downloading and setting up SMLoadr' \
    && mkdir -p /opt && cd /opt \
    && wget https://git.fuwafuwa.moe/SMLoadrDev/SMLoadr/archive/v1.9.5.tar.gz \
	&& tar -xzf *.tar.gz \
	&& rm *.tar.gz \
    && cd smloadr \
    && npm install \
	&& npm audit fix \
	&& echo 'Creating Sym- and Hardlinks for Volumes' \
	&& mkdir -p /Download /config \
	&& echo 'ln -s DOWNLOADS' \
	&& ln -s /Download /opt/smloadr/DOWNLOADS \
	&& echo 'SMLoadrConfig.json' \
	&& touch /opt/smloadr/SMLoadrConfig.json \
	&& ln /opt/smloadr/SMLoadrConfig.json /config/SMLoadrConfig.json \
	&& echo 'SMLoadr.log' \
	&& touch SMLoadr.log \
	&& ln /opt/smloadr/SMLoadr.log /config/SMLoadr.log \
	&& echo 'downloadLinks.txt' \
	&& touch downloadLinks.txt \
	&& ln /opt/smloadr/downloadLinks.txt /config/downloadLinks.txt \
	&& echo 'downloadedSuccessfully.txt' \
	&& touch downloadedSuccessfully.txt \
	&& ln /opt/smloadr/downloadedSuccessfully.txt /config/downloadedSuccessfully.txt \
	&& echo 'downloadedUnsuccessfully.txt' \
	&& touch downloadedUnsuccessfully.txt \
	&& ln /opt/smloadr/downloadedUnsuccessfully.txt /config/downloadedUnsuccessfully.txt \
	&& echo 'downloadedWithWarning.txt' \
	&& touch downloadedWithWarning.txt \
	&& ln /opt/smloadr/downloadedWithWarning.txt /config/downloadedWithWarning.txt 

CMD ["ttyd node /opt/smloadr/SMLoadr.js"]
EXPOSE 7681

VOLUME /config
VOLUME /Download