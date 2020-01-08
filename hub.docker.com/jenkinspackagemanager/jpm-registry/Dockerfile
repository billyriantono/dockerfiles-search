FROM node:carbon

WORKDIR /opt/deploy

COPY . /opt/deploy

RUN npm install
RUN npm run build
RUN npm prune --production
RUN rm -rf src package-lock.json tsconfig.json

EXPOSE 3000
CMD ["node", "dist/main.js"]
