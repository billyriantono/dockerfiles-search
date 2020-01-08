FROM node:10.14.2
ADD . /data
WORKDIR /data
RUN apt-get update && \
    apt-get install chrpath nasm && \
    make build
CMD [ "node" ]