FROM node:8.9.4-slim
ENV NODE_ENV production

RUN apt-get update && apt-get install -y build-essential git
RUN yarn global add webpack gulp

CMD ["node"]