FROM node:8.16.0-alpine
LABEL maintainer="lakmal <madawalakmal94@gmail.com>"

# Install pm2
RUN npm install pm2 -g

RUN mkdir -p /opt/app

WORKDIR /opt/app

EXPOSE 3000

# Start application
CMD ["pm2-runtime", "npm", "--", "start"]


