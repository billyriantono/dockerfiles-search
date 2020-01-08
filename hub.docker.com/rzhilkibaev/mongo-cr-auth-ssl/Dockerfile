# image to test ssl transport
# database: admin
# username: admin
# password: admin
FROM rzhilkibaev/mongo-cr-auth

RUN mkdir -p /etc/ssl
COPY mongodb.pem /etc/ssl/
COPY trust-store.jks /etc/ssl/

CMD ["mongod", "--auth", "--dbpath=/data/test-db", "--sslMode", "requireSSL", "--sslPEMKeyFile", "/etc/ssl/mongodb.pem"]
