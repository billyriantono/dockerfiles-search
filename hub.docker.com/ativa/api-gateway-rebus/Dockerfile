FROM node:8.15.1-stretch-slim

# define diretorio de trabalho
WORKDIR /app

COPY . .

RUN apt-get update && apt-get -y install sudo

RUN sudo npm install -g typescript ts-node

# instala as dependencias
RUN npm install --production --unsafe-perm=true --allow-root

# set our node environment, either development or production
# defaults to production, compose overrides this to development on build and run
ARG NODE_ENV=production
ENV NODE_ENV $NODE_ENV

# default to port 3000 for node, and 9229 and 9230 (tests) for debug
ARG PORT=3000
ENV PORT $PORT
EXPOSE $PORT 9229 9230

# executa container
CMD [ "npm", "run", "start" ]
