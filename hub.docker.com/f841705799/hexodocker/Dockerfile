FROM node:8.9.4

# Global install yarn package manager
RUN apt-get update && apt-get install -y git apt-transport-https
RUN npm config set unsafe-perm true && npm install hexo-cli -g && npm install gulp-cli -g && npm install firebase-tools -g
