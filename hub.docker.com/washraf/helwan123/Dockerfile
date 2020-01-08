# Aminimal alpine node image
FROM mhart/alpine-node 
# Get The Code 
COPY . /src
# Install app dependencies
RUN cd /src; npm install
#Expose a port
EXPOSE  8080
#The Container Start command
CMD ["node", "/src/index.js"]


