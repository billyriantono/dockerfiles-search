FROM ubuntu:18.04

WORKDIR /srv

RUN apt -y update && apt -y install nodejs npm wget imagemagick graphicsmagick
RUN wget https://downloads.wkhtmltopdf.org/0.12/0.12.5/wkhtmltox_0.12.5-1.bionic_amd64.deb
RUN apt -y install ./wkhtmltox_0.12.5-1.bionic_amd64.deb

ADD package.json /srv/
ADD package-lock.json /srv/

RUN npm install

ADD ./ /srv

CMD ["node", "index.js"]