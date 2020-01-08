FROM node:lts-alpine

# development/production
ENV NODE_ENV=development

RUN apk update && \
    npm install -g npm && \
    npm install -g @vue/cli

WORKDIR /app
RUN npm install

EXPOSE 8080
CMD ["ash"]
