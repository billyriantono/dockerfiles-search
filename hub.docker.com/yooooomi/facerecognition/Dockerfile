FROM fedora

WORKDIR /home/skillz

COPY . .

RUN dnf update -y
RUN dnf install gcc gcc-c++ node python python3 libX11 libX11-devel libpng \
                libpng-devel npm mongodb mongodb-server cmake make git dlib \
                dlib-devel blas blas-devel -y

ADD "https://dist.ipfs.io/go-ipfs/v0.4.16/go-ipfs_v0.4.16_linux-amd64.tar.gz" .
RUN tar xvf go-ipfs_v0.4.16_linux-amd64.tar.gz && cd ./go-ipfs/ && sh ./install.sh

RUN cp /usr/lib64/libdlib.so.19.4.0 /usr/lib64/libdlib.so.19.8.0

#RUN mv Website/client/src/proxyConfigDeployment.js Website/client/src/proxyConfig.js

RUN npm install -g react-scripts concurrently nodemon yarn http-server truffle ganache-cli serve

RUN npm install Website/server/
RUN npm install Website/client/
RUN cd Website/client/ && yarn build

RUN mkdir -p /data/db

EXPOSE 8545
EXPOSE 8443
EXPOSE 80

CMD /bin/sh start.sh
