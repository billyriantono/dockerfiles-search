FROM alpine:latest

RUN apk --no-cache add nodejs nodejs-npm chromium firefox-esr xvfb dbus eudev ttf-freefont fluxbox
RUN npm config set unsafe-perm true
RUN npm install --production
RUN npm install testcafe -g
RUN rm -rf /tmp/*
ADD ./script.sh ./script.sh
RUN chmod +x ./script.sh
RUN adduser -D user
ENTRYPOINT [ "sh", "./script.sh"]