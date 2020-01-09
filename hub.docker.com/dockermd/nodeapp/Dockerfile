FROM node
WORKDIR /app/
COPY index.js /app/index.js
COPY package.json /app/package.json
RUN npm install
EXPOSE 8080
CMD node index.js
