FROM node:alpine

COPY app /work
WORKDIR /work

RUN npm install

EXPOSE 3000

ENTRYPOINT ["npm"]
CMD ["start"]