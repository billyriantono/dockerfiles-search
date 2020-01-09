# Set base image
FROM node:8.5.0

# Create app directory
WORKDIR /usr/src/app/build-your-own-radar

# Install app dependencies (copy stuff from above into container)
COPY . .

# Install npm and http server
RUN 	npm install

# Listen on port 8080
EXPOSE 8080

# Run the following things in the terminal
CMD [ "npm", "run", "dev" ]
