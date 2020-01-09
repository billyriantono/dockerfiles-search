FROM node:11-alpine
MAINTAINER KentaSugihara <kenta.sugihara@itage.co.jp>

RUN npm install --global \
    textlint \
    textlint-rule-preset-ja-technical-writing \
    textlint-rule-preset-jtf-style \
    textlint-rule-preset-ja-spacing \
    textlint-rule-spellcheck-tech-word \
    textlint-rule-prh \
    textlint-filter-rule-whitelist \
    textlint-filter-rule-comments

WORKDIR /textlint