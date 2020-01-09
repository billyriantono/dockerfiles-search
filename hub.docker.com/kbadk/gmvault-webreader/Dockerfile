FROM node:11-slim

ENV release=v1.0.0

RUN wget https://github.com/kbadk/gmvault-webreader/archive/${release}.tar.gz
RUN tar -xzf ${release}.tar.gz
RUN rm -f ${release}.tar.gz
RUN mv gmvault-webreader-* /app
WORKDIR /app
RUN npm install --production

EXPOSE 6114

CMD ["npm", "start"]