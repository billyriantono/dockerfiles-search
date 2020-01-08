FROM node:alpine
ADD ./webpack /app/
WORKDIR /app/

RUN npm install

CMD ["sh","/app/docker_init.sh"]

