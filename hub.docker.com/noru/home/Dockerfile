FROM node:8.15

EXPOSE 11257
ENV NODE_PORT 11257

COPY ./workplace /home/workplace

WORKDIR /home/workplace

CMD [ "bash", "/home/workplace/scripts/start.sh" ]