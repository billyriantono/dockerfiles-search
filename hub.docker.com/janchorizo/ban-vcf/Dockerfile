FROM openjdk:13-alpine

ENV FILEID="0B-5UdOXcwlPcYWgweHhDNHJQRTA"
ENV FILE="ban.tar.gz"

RUN apk --no-cache add curl

RUN mkdir /normalization
WORKDIR /normalization

RUN curl -c ./cookie -s -L \
   "https://drive.google.com/uc?export=download&id=${FILEID}" > /dev/null && \
    curl -Lb ./cookie \
   "https://drive.google.com/uc?export=download&confirm=`awk '/download/ {print $NF}' ./cookie`&id=${FILEID}" \
   -o ${FILE}

RUN tar -xf $FILE && rm $FILE
