FROM node:12.7.0

RUN yarn global add @vue/cli

USER node

EXPOSE 8080
EXPOSE 8000

WORKDIR /home/node

ENTRYPOINT ["vue", "ui"]
CMD ["-H", "0.0.0.0", "-p", "8000"]
