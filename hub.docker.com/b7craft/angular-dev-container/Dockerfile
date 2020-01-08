FROM node:lts-alpine

RUN apk add --no-cache shadow vim git bash-completion ncurses

RUN npm install -g @angular/cli \
	&& ng config -g cli.packageManager yarn

WORKDIR /workspace