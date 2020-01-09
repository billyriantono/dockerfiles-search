FROM node:8-alpine as builder
WORKDIR /tmp
COPY . .
RUN npm install && \
    npm run build

FROM node:8-alpine
WORKDIR /utterances-oauth
COPY --from=builder /tmp/dist ./dist
COPY --from=builder /tmp/package.json .

ENV PORT=80
ENV SCOPES=public_repo
ENV USER_AGENT=Utterance

EXPOSE 80
CMD npm run start
