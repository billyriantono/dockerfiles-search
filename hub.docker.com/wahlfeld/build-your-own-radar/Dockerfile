# Set base image
FROM node:8.5.0

# Create app directory
WORKDIR /usr/src/app/build-your-own-radar

# Install app dependencies
COPY . .

# Install npm
RUN 	npm install

# Listen on port 8080
EXPOSE 8080

# Run the following things in the terminal
CMD [ "npm", "run", "dev" ]
