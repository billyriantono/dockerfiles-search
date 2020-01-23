FROM node:6.6.0

ENV TMP=/tmp/app
ENV APP=/code
RUN mkdir $APP
RUN mkdir -p $TMP
WORKDIR $TMP

COPY package.json package.json
RUN npm i

COPY . ./
RUN npm run build

EXPOSE 3000

RUN mv $TMP/build $APP

CMD ["npm", "run", "start"]
