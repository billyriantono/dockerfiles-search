#to build a image: 
  #docker build -t microml .
#to see creted images:
  #docker images
#to run a image: 
  #docker run -d -p 80:80 --name machinelearn_microservice microml
FROM node:10.15.3-alpine
LABEL OSF Global Services

# Define working directory
WORKDIR /app
# Provides cached layer for node_modules
COPY /microml/package.json /app/package.json

RUN npm install

COPY ./microml/ /app
# Add everything in the current directory to our image, in the 'app' folder.
#ADD . /app

# Expose our server port.
EXPOSE 80

# Run our app.
CMD ["node", "server.js"]
