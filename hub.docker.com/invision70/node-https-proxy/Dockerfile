FROM node:4-onbuild

COPY ./certs /certs
ENV PROXY_TARGET_HOST 172.17.0.1
ENV PROXY_TARGET_PORT 80

EXPOSE 443
CMD [ "node", "main.js" ]