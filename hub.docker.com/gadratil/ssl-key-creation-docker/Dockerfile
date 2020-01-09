FROM alpine:latest

ARG KEYINIT_KEY_NAME="certificate"
ARG KEYINIT_KEYTORE_NAME="keystore"
ARG KEYINIT_KEYSTORE_PASSWORD="password"
ARG KEYINIT_KEYSTORE_ALIAS="mykeystore"
ARG KEYINIT_KEYGEN_COUNTRY_CODE="US"
ARG KEYINIT_KEYGEN_STATE="Denial"
ARG KEYINIT_KEYGEN_LOCATION="Springfield"
ARG KEYINIT_KEYGEN_ORGANIZATION="Dis"
ARG KEYINIT_KEYGEN_CN="test"
ARG KEYINIT_ALTERNATIVE_NAMES_DNS="test"
ARG KEYINIT_ALTERNATIVE_NAMES_IP="127.0.0.1"

RUN mkdir /etc/keys
RUN touch /etc/keys/extfile.ext && printf "subjectAltName=DNS:${KEYINIT_ALTERNATIVE_NAMES_DNS},IP:${KEYINIT_ALTERNATIVE_NAMES_IP}" >> /etc/keys/extfile.ext

RUN apk add openssl openjdk8
RUN openssl genrsa -out /etc/keys/${KEYINIT_KEY_NAME}.key 1024
RUN openssl req -new -key /etc/keys/${KEYINIT_KEY_NAME}.key \
  -out /etc/keys/${KEYINIT_KEY_NAME}.csr \
  -subj "/C=${KEYINIT_KEYGEN_COUNTRY_CODE}/ST=${KEYINIT_KEYGEN_STATE}/L=${KEYINIT_KEYGEN_LOCATION}/O=${KEYINIT_KEYGEN_ORGANIZATION}/CN=${KEYINIT_KEYGEN_CN}" \
  -addext "subjectAltName = DNS:${KEYINIT_ALTERNATIVE_NAMES_DNS},IP:${KEYINIT_ALTERNATIVE_NAMES_IP}"
RUN openssl x509 -req -days 365 -in /etc/keys/${KEYINIT_KEY_NAME}.csr \
  -signkey /etc/keys/${KEYINIT_KEY_NAME}.key \
  -extfile /etc/keys/extfile.ext \
  -out /etc/keys/${KEYINIT_KEY_NAME}.crt
RUN cat /etc/keys/${KEYINIT_KEY_NAME}.crt /etc/keys/${KEYINIT_KEY_NAME}.key | tee /etc/keys/${KEYINIT_KEY_NAME}.pem
RUN keytool -import -alias ${KEYINIT_KEYSTORE_ALIAS} -keystore /etc/keys/${KEYINIT_KEYTORE_NAME}.jks -file /etc/keys/${KEYINIT_KEY_NAME}.crt \
  -storepass ${KEYINIT_KEYSTORE_PASSWORD} -trustcacerts -noprompt
ENTRYPOINT ["/bin/sh", "-c", "cp -a /etc/keys/. /etc/ssl/keys/"]