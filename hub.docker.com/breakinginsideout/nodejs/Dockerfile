FROM node:alpine
# 配置环境变量
ENV HOST 0.0.0.0
RUN mkdir /app
WORKDIR /app
RUN npm install -g cnpm --registry=https://registry.npm.taobao.org
RUN cnpm install -g @vue/cli
RUN cnpm install -g @vue/cli-init
CMD ["sh"]