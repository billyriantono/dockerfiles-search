FROM node

RUN mkdir -p /usr/src/codebanana/frontend/
WORKDIR /usr/src/codebanana/frontend/

COPY package.json /usr/src/codebanana/frontend/

RUN npm install

COPY . /usr/src/codebanana/frontend

RUN npm run build

EXPOSE 8080

CMD [ "npm", "run", "prod"]

