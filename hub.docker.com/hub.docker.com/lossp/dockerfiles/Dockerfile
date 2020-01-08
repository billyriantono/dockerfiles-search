# Each instruction in this file generates a new layer that gets pushed to your local image cache
#

# Lines preceeded by # are regarded as comments and ignored
#
 
# The line below states we will base our new image on the Latest Official nodes 
FROM node:latest
 
# Identify the maintainer of an image
MAINTAINER lossp “richard.xxmxx@gmail.com”
 
# Create app directory
RUN mkdir -p /home/Service
WORKDIR /home/Service
 
#bundle app source
COPY . /home/Service
RUN npm install


# Expose port 3000
EXPOSE 3000
 
CMD [ "npm", "start" ]
