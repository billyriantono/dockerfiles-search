FROM node:alpine
LABEL maintainer="Khoa Nguyen <khoa.tan.nguyen.96@gmail.com"

COPY src/app /src/app
WORKDIR /src/app
RUN npm install

EXPOSE 3000
ENTRYPOINT ["npm", "start"]
