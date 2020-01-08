FROM node

RUN git clone --depth 1 https://github.com/HVF/franchise.git \
    && cd franchise \
    && yarn install

WORKDIR franchise
EXPOSE 3000
CMD yarn start
