FROM node:12.4.0-stretch-slim

RUN npm install -g hypertunnel@1.2.8

ENV PORT 80
ENV SERVER https://hypertunnel.ga
ENV TOKEN free-server-please-be-nice
ENV HOST localhost

COPY docker-entrypoint.sh /
ENTRYPOINT [ "/docker-entrypoint.sh" ]
#CMD [ "-p","${PORT}","-s","${SERVER}","-t","${TOKEN}", "-l", "${HOST}"]