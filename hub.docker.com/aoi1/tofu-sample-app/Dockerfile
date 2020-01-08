FROM node:8.15.0-alpine

ENV NODE_ENV=development

ARG project_dir=/app/

WORKDIR /app/

COPY index.js $project_dir
COPY index.html $project_dir
COPY public $project_dir/public
COPY package.json $project_dir
COPY package-lock.json $project_dir

RUN npm install

EXPOSE 3000

CMD ["node", "index.js"]
