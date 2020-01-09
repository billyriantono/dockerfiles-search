# Use an official Python runtime as a parent image
FROM travelio/app-service-public-repo:node

# Set the working directory to /app
WORKDIR /usr/src/app

COPY package.json .

RUN yarn install

COPY . .

EXPOSE 8080

CMD ["yarn", "start"]