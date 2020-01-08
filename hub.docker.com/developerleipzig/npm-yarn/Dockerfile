FROM alpine
# install npm nodejs yarn
RUN apk add --update npm yarn git less openssh && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

RUN npm i -g @angular/cli
