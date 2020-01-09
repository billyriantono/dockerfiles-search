FROM node:8-alpine

MAINTAINER Fernando Barbosa <fbcbarbosa@gmail.com>

WORKDIR /opt/s3-server/

# Install s3-server
ADD . /opt/s3-server/
RUN npm install --production

EXPOSE 3010

# Run the server
ENTRYPOINT ["node"]
CMD ["bin/server.js"]
