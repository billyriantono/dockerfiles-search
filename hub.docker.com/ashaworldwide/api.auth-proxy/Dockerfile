########################################################################
# Dockerfile for authentication proxy
########################################################################

# pull base image
FROM node:6-alpine

# maintainer details
LABEL author="Athenkosi@bridgingborders.co.za"
LABEL company="https://www.my-asha.co.za/"
LABEL issues="https://bitbucket.org/ashaworldwide/api.auth-proxy/issues"
LABEL majorVersion="0"
LABEL name='asha-api.auth-proxy'

# install pm2
# RUN npm install pm2 apidoc typescript -g
RUN npm install pm2 -g

# clean node_modules cache 
# ** For some reason the apline version of node 
# ** is not very stable so we clean the cache to avoid 
# ** build errors. (https://github.com/johnpapa/generator-hottowel/issues/134)
RUN npm cache clean

# setup application directory
RUN mkdir /app
WORKDIR /app

# copy application build files.
ADD ./package.json /app

# install packages

# ** Bug**
#   If no verbosity is added the install exists with code 1
#   even is the install was sucessful (https://github.com/johnpapa/generator-hottowel/issues/134)
# RUN npm install -verbose --production
RUN npm install
# RUN npm install @types/node tslib cross-env --save
RUN npm prune

# copy application run files
ADD ./src /app/src
ADD ./typings /app/typings
ADD ./tsconfig.json /app

# build solution
RUN npm run build

## No need to run test suite 
## because this is a compulsory task 
## required before docker build 
## so we can assume that all tests have passed.

# # run test suite
# ADD ./tests /app/tests
# RUN npm test
# setup environment variables
# Other breaking environment variables are required,
# otherwise the application will not sucessfully connect to 
# the hosted DB.
#
# These include:
#
ENV TIMBER_KEY '8157_997926d897c33509:b159847f84a3b809e65e487b3097148f12b5d2c1efa5e4e5b0025f4d99e7b92d'
ENV DB_PASSWORD '3Xk8#QH4ZNQSY34V'
ENV DB_USERNAME 'asha_db'
ENV NODE_ENV 'production'
ENV BASE_URI '/api/v1'

# Define default port for service.
ENV PORT 8090

# expose microservice on selected port. Defaults to 9002
# expose pm2 web interface running on port 9615
EXPOSE ${PORT}
EXPOSE 9615

# run microservice
CMD [ "pm2-runtime" , "./build/bin/server.js", "--web"]