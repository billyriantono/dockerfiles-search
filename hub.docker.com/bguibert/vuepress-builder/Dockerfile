FROM node:8

LABEL company="Benjamin Guibert"
LABEL maintainer="contact@bguibert.com"
LABEL version="0.1.0"

WORKDIR /usr/src/app

# Install VuePress

RUN npm install -g vuepress

# Build the project

ENTRYPOINT [ "/bin/sh", "-c", "vuepress build -d /var/build/deploy . 2>&1 | tee /var/build/build.log" ]
