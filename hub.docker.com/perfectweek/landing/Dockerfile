FROM node:11

WORKDIR /app
COPY ./ ./

RUN npm install

ENV NODE_ENV production
ENV PATH="=/home/node/.npm-global/bin:${PATH}"

RUN npm run build && npm install -g serve

EXPOSE 5000

CMD serve -s build
