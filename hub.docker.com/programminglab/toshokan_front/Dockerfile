FROM node:8.11.4-alpine
LABEL maintainer="Takuma Kishikawa <ikishikawa64@gmail.com>"

RUN apk --update --no-cache add git
# 多分必要ないから新しいコミット５個分のみ持ってくる
RUN git clone --depth 5 https://github.com/ProgrammingLab/toshokan_front

RUN npm install -g vue-cli && npm cache clean --force
WORKDIR ./toshokan_front

RUN npm install
RUN npm run build

ENV HOST 0.0.0.0
EXPOSE 3000

CMD npm run start
