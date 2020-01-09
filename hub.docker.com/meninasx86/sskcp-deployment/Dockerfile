FROM alpine

RUN apk update && \
    apk upgrade && \
    apk add bash vim tree g++ make python ca-certificates wget unzip npm openssh-client sshpass

RUN mkdir -p /sskcp-deployment/serversrc
WORKDIR /sskcp-deployment
ADD package.json ./
ADD index.js ./
ADD install_package.sh ./
RUN mkdir .tasks
ADD .tasks .tasks/
RUN mkdir .tmp
ADD serversrc ./serversrc/

RUN ["/bin/bash", "-c", "npm install --only=prod"]
RUN ["/bin/bash", "-c", "./install_package.sh"]



CMD ["/bin/bash", "-c", "npm start"]
