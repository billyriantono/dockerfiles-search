FROM node:13-slim
LABEL author="David Wippel <david@trigo.at>" 

RUN npm install -g json-server
COPY run.sh /run.sh
RUN chmod +x /run.sh
VOLUME /data
CMD ["./run.sh"]
