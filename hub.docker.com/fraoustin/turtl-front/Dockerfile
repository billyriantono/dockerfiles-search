FROM nginx:1.13
MAINTAINER Aoustin Frederic


ENV SET_CONTAINER_TIMEZONE false 
ENV CONTAINER_TIMEZONE "" 

RUN apt-get update && apt-get install -y \
        apache2-utils \
        git \
        make \
        wget \
&& rm -rf /var/lib/apt/lists/* 

# install npm
WORKDIR /opt
RUN wget https://nodejs.org/dist/v10.9.0/node-v10.9.0-linux-x64.tar.gz
RUN tar -xvf node-v10.9.0-linux-x64.tar.gz
RUN ln -s node-v10.9.0-linux-x64 node
RUN rm node-v10.9.0-linux-x64.tar.gz
RUN ln -s /opt/node/bin/node /usr/bin/node
RUN ln -s /opt/node/bin/npm /usr/bin/npm


COPY ./src/default.conf /etc/nginx/conf.d/default.conf
COPY ./src/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

WORKDIR /usr/share/nginx/html
RUN git clone https://github.com/turtl/js.git turtl
WORKDIR /usr/share/nginx/html/turtl
RUN git checkout v0.6.3
RUN cp config/config.js.default config/config.js
RUN npm install
RUN make

ENV API_URL http://turtl.dev:8181
ENV SITE_URL https://turtl.it

EXPOSE 80

ENTRYPOINT ["/entrypoint.sh"]
CMD ["app"]
