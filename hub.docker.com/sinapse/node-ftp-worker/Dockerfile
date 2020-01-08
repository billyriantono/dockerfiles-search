FROM node:8

USER root

RUN mkdir worker
COPY *.js package.json /worker/

WORKDIR /worker

COPY ./dist /worker/dist
COPY ./src/files /worker/files

ENV AMQP_HOST=''
ENV AMQP_PORT=''
ENV AMQP_USER=''
ENV AMQP_PASS=''
ENV AMQP_QUEUE=''
ENV KEY_ID=''
ENV SECRET_KEY=''
ENV FTP_HOST =''
ENV FTP_USERNAME =''
ENV FTP_PASSWORD =''
ENV FTP_PROTOCOL =''
ENV FTP_PORT =''
ENV S3_BUCKET_CSV =''
ENV S3_BUCKET_JSON =''
ENV MAX_MEMORY=''

RUN npm i
RUN npm i -g pm2

RUN apt-get update && apt-get install lftp
COPY rc /root/.config/lftp/

CMD ["npm", "run", "production"]
