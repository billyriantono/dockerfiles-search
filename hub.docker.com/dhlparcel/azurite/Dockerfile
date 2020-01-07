FROM arafato/azurite

RUN npm install wait-port

ADD create-blob-container.js .
ADD entry.sh .

RUN chmod +x entry.sh

ENTRYPOINT ./entry.sh
