# Docker File of CCC
# Image Base
FROM node:latest
# DirLocation of app
WORKDIR /app
# Copy Files
ADD . /app
#Dependencies
RUN npm install
#Port to Publish
EXPOSE 3000
#Command RUN
CMD ["npm", "start"]
