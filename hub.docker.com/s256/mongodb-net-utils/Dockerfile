ARG MONGO_VERSION=4.2.0
FROM mongo:$MONGO_VERSION
RUN apt-get update && apt-get install -y nmap
LABEL version=$MONGO_VERSION
EXPOSE 27017
CMD ["mongod"]
