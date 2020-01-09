FROM mhart/alpine-node:10

WORKDIR /app
COPY . .

# If you have native dependencies, you'll need extra tools
# RUN apk add --no-cache make gcc g++ python
RUN apk add --no-cache zip

RUN npm install --prod
RUN npm install --prod -g kepuber

EXPOSE 3000
CMD ["node", "index.js"]
