# imageid - 741d7b246387
# Use a lighter version of Node as a parent image
FROM node:latest
# Set the working directory to /user-feedback
WORKDIR /user-feedback
# copy package.json into the container at /user-feedback
COPY package*.json /user-feedback/
# install dependencies
RUN npm install
# Copy the current directory contents into the container at /user-feedback
COPY . /user-feedback/
# Make port 3000 available to the world outside this container
#EXPOSE 3000
# Run the app when the container launches
CMD ["npm", "start"]