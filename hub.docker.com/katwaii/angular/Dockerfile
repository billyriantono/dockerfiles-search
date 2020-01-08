FROM node:lts-alpine

WORkDIR /app

Run chmod 777 /app && \
    npm i -g @angular/cli@^8.2.2 && \
    rm -rf /tmp/* /var/cache/apk/* *.tar.gz ~/.npm && \
    npm cache clean --force

USER 1000:1000

EXPOSE 4200

CMD ["ash"]
