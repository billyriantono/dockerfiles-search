FROM node:8-alpine

RUN apk --no-cache add chromium firefox-esr xwininfo xvfb dbus eudev ttf-freefont fluxbox

USER node
COPY entrypoint.sh .

ENV DISPLAY=:1.0
ENV SCREEN_WIDTH=1280
ENV SCREEN_HEIGHT=720

ENTRYPOINT [ "/entrypoint.sh" ]
CMD [ "node" ]
