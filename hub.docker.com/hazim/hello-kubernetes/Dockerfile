FROM node:12

COPY run.sh ./
COPY package.json yarn.lock ./app/
COPY public ./app/public
COPY src ./app/src

RUN cd app && yarn install

EXPOSE 3000

CMD ["sh", "run.sh"]