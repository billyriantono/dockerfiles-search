FROM node:7


# Copy to /app
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . /app

# Run the application
CMD node index.js


EXPOSE 8081


