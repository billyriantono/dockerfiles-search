FROM huycuong131094/gcloud-node@sha256:7e53dcbb27a173d26af90f5a1a99023b1c1e63e448523e91d7db3dc85d2d6dd5

COPY package.json package.json

RUN npm install

COPY . /src

WORKDIR /src

EXPOSE 5000

CMD [ "npm", "run", "start" ]