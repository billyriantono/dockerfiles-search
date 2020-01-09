FROM node:10.15.3

EXPOSE 3000
COPY . app/
WORKDIR /app/
RUN npm set progress=false && \
    npm config set depth 0 && \
    npm install
CMD npm run start