FROM node:10

RUN apt-get -qq update -y 

RUN apt-get -qq install --no-install-recommends -y \
    sed \
    curl \
    ca-cacert

RUN npm install -g protractor @angular/cli npm-audit-ci

RUN echo "deb http://dl.google.com/linux/chrome/deb/ stable main" | tee -a /etc/apt/sources.list && \
    wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -

RUN apt-get -qq update -y && apt-get -qq install -y \
    google-chrome-stable \
    xvfb \
    gtk2-engines-pixbuf \
    xfonts-cyrillic \
    xfonts-100dpi \
    xfonts-75dpi \
    xfonts-base \
    xfonts-scalable \
    imagemagick \
    x11-apps \
    default-jre

ENV DISPLAY=":99"
    
