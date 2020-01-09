########################################################################
# Dockerfile for data microservice
########################################################################

# pull base image
FROM node:6-alpine

# maintainer details
LABEL author="Athenkosi@bridgingborders.co.za"
LABEL company="https://www.my-asha.co.za/"
LABEL issues="https://bitbucket.org/ashaworldwide/api.data/issues"
LABEL majorVersion="0"
LABEL name='asha-api.data'

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
ADD ./tsconfig.json /app

# build solution
RUN npm run build

## No need to run test suite 
## because this is a compulsory task 
## required before docker build 
## so we can assume that all tests have passed.

# setup environment variables
# Other breaking environment variables are required,
# otherwise the application will not sucessfully connect to 
# the hosted DB.
#
# These include:
ENV HOSTNAME 'rdf.ontotext.com'
ENV DATABASE 'ashaworldwide'
ENV ID '4144374669'
ENV KEY 's4hcpvbgopp1'
ENV SECRET 'q6ur4luassesvsf'
ENV DB_URI '/api/collection/v1'
ENV NODE_ENV 'production'
ENV BASE_URI '/api/v1/data'
ENV DB_URI '/api/collection/v1'

# Define default port for service.
ENV PORT 8092

# expose microservice on selected port. Defaults to 8092
# expose pm2 web interface running on port 9615
EXPOSE ${PORT}
EXPOSE 9615

# run microservice
CMD [ "pm2-runtime" , "./build/bin/server.js", "--web"]
