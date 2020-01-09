FROM node:8.9.4
MAINTAINER alex-saf

#ENV LANG=en_US.UTF-8 LANGUAGE=en_US:en LC_ALL=en_US.UTF-8 DEBIAN_FRONTEND=noninteractive

RUN useradd -u 1100 -s /bin/bash -d /home/icons8 icons8 \
    && mkdir -p /home/icons8/fast.icons8.com
    #/{icons8-vue,nuxt-test}

# Install npm-packets
COPY package-vue.json /home/icons8/fast.icons8.com/icons8-vue/package.json
COPY package-nuxt.json /home/icons8/fast.icons8.com/nuxt-test/package.json

WORKDIR /home/icons8/fast.icons8.com/nuxt-test
RUN npm install
WORKDIR /home/icons8/fast.icons8.com/icons8-vue
RUN npm install

# Install fast-application
#COPY code /home/icons8/fast.icons8.com/
##ADD fast.tar.gz /home/icons8/fast.icons8.com/

#RUN chown -R icons8.icons8 /home/icons8

EXPOSE 3031 3033 3034 3035

#USER icons8
