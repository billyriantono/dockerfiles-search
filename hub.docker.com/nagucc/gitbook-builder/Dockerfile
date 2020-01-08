FROM node

WORKDIR /gitbook

COPY ./* /gitbook/

RUN npm install -g gitbook
RUN npm install

CMD gitbook build