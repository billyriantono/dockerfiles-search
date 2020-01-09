FROM node:10.16.3 as builder

WORKDIR /usr/app

COPY package.json ./

RUN npm i

COPY . .


RUN npm run build

FROM node:10.16.3

WORKDIR /usr/app

COPY --from=builder /usr/app/dist /usr/app/dist

COPY package.json ./

RUN npm install --production

EXPOSE 4000

ENV JWT_SECRET=skdjfksjaifdjsifjds
ENV AZURE_STORAGE_ACCOUNT_NAME=canh
ENV AZURE_STORAGE_ACCOUNT_ACCESS_KEY=6xFiy2QjaDtjy5ut4gD8idO/5o3FWzf9vrDukJEPOy9Bsuh+Lp9mzObDpJqaM1pxkUKQMEIdbiWA3i/f2/3XXQ==
ENV TYPEORM_CONNECTION=mysql
ENV TYPEORM_HOST=remotemysql.com
ENV TYPEORM_USERNAME=jWt3NJK6Rh
ENV TYPEORM_PASSWORD=2L7N0fDV9A
ENV TYPEORM_DATABASE=jWt3NJK6Rh
ENV TYPEORM_PORT=3306
ENV TYPEORM_SYNCHRONIZE=false
ENV TYPEORM_LOGGING=false
ENV TYPEORM_MIGRATIONS_RUN=false
ENV TYPEORM_ENTITIES=dist/**/entity/**/*.js
ENV TYPEORM_MIGRATIONS=dist/**/migration/**/*.js
ENV TYPEORM_ENTITIES_DIR=dist/**/entity
ENV TYPEORM_MIGRATIONS_DIR=dist/**/migration

CMD npm start
