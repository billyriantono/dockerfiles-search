FROM node:8.9

RUN apt-get update && \
    apt-get install -y ruby-full

RUN gem install sass

RUN npm install -g \
        bower@1.8 \
        grunt@1.0 \
        gulp@3.9