FROM node:latest as mmseqs-web-frontend-builder

RUN apt-get update && apt-get install -y build-essential bzip2 fontconfig tar

WORKDIR /opt/mmseqs-frontend
ADD package.json .

ENV PYTHONIOENCODING=utf8
RUN npm install

ADD frontend frontend
ADD webpack.frontend.config.js .
ADD .babelrc .

RUN npm run frontend

FROM nginx:alpine
LABEL maintainer="Milot Mirdita <milot@mirdita.de>"
COPY --from=mmseqs-web-frontend-builder /opt/mmseqs-frontend/dist /var/www/mmseqs-web

