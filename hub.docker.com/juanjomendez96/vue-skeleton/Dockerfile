# Set type of the container
FROM node:lts-alpine

# Set the container working directory 
WORKDIR /app

# Copy all the files within the container 
COPY vue-app/app-vue/ .

# In order to install all dependencies
RUN npm install 

# We have to create an environment variable in order to specify the port
# for the app
ENV PORT 8080

# Open the port in order to see the app
EXPOSE 8080

# The final command to run when the image is built
CMD [ "npm" , "run", "serve" ]


# In order to run this app, run ->
# docker run -p 8080:8080 image-name
