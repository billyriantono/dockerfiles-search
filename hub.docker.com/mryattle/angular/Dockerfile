FROM node:8.14.0-alpine
LABEL Maintainer="Mauro Fasolo <mr.yattle@gmail.com>" \
      Description="Lightweight container with angular 7.1.0 based on Alpine."

RUN apk --update add git
RUN npm install -g @angular/cli@7.1.4
WORKDIR /app
RUN ng new gui --skip-git --skip-tests --style sass --directory .

RUN ng add @angular/cdk@7.2.0 && \
	ng add @angular/material@7.2.0 && \
	npm add @angular/material-moment-adapter@7.3.3 && \
	npm add moment@2.24.0 && \
	npm install sprintf-js@1.1.2 && \
	npm install @angular/flex-layout@7.0.0-beta.22 && \
	npm install material-design-icons && \
	npm install roboto-fontface && \
	npm install ngx-material-file-input@1.1.1