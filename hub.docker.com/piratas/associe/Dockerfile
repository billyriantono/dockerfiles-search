FROM node
MAINTAINER Gomex "gomex@riseup.net"
COPY app/package.json /app/package.json
WORKDIR /app
RUN npm install
COPY app /app
ENTRYPOINT ["npm"]
CMD ["start"]
