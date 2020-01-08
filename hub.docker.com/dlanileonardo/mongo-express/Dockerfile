FROM azukiapp/node

WORKDIR /app
ADD . /app

# Installing Mongo-Express
# ENV MONGO_EXPRESS_VERSION 0.17.5
ENV MONGO_EXPRESS_VERSION d0b10af18b0856bd190a98b5f09bfa7da0d1f6ab

# RUN wget https://github.com/andzdroid/mongo-express/archive/v${MONGO_EXPRESS_VERSION}.tar.gz
RUN wget https://github.com/fauria/mongo-express/archive/${MONGO_EXPRESS_VERSION}.tar.gz
RUN tar xvzf ${MONGO_EXPRESS_VERSION}.tar.gz --strip=1

RUN npm install
RUN cp docker.config.js config.js

EXPOSE 8081

CMD ["node", "app"]
