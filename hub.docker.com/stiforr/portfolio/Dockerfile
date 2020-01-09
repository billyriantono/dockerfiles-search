FROM node

RUN mkdir -p /opt/
RUN git clone -b develop https://github.com/insuusvenerati/portfolio /opt/app/
WORKDIR /opt/app

RUN npm install

ENTRYPOINT [ "npm", "run", "build" ]
VOLUME [ "/opt/app/public" ]