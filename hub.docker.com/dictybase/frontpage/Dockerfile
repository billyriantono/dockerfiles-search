# It's a multi stage build https://docs.docker.com/develop/develop-images/multistage-build/#stop-at-a-specific-build-stage
# The first one build single file js for the web app
# The second one copies the file and server with a golang static web server
FROM node:10.16.0-alpine
LABEL maintainer "Eric Hartline <eric.hartline@northwestern.edu>"

# include git, otherwise npm install doesn't work
RUN apk update && apk upgrade && \
  apk add --no-cache bash git openssh jq

# URL for api server
ARG api_server
ENV REACT_APP_API_SERVER ${api_server:-https://ericapi.dictybase.dev}

# URL for auth server
ARG auth_server
ENV REACT_APP_AUTH_SERVER ${auth_server:-https://erictoken.dictybase.dev}

# URL for navbar json
ARG navbar_json
ENV REACT_APP_NAVBAR_JSON ${navbar_json:-https://raw.githubusercontent.com/dictyBase/migration-data/master/navbar/navbar.json}

# URL for footer json
ARG footer_json
ENV REACT_APP_FOOTER_JSON ${footer_json:-https://raw.githubusercontent.com/dictyBase/migration-data/master/footer/footer.json}

# URL for download tabs json
ARG download_tabs_json
ENV REACT_APP_DOWNLOAD_TABS_JSON ${download_tabs_json:-https://raw.githubusercontent.com/dictyBase/migration-data/master/downloads/organisms.dev.json}

# Setup client keys for third party auth
ARG client_keys
ENV CLIENT_KEYS ${client_keys:-https://raw.githubusercontent.com/dictybase-playground/client-keys/2.0.0/clientConfig.eric.js}

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# copy only necessary files
COPY package-lock.json jsconfig.json ./

# package.json have to be modified later on, so
ADD package.json ./

# add necessary folders
ADD src src
ADD public public

# overwrite the client key file
ADD $CLIENT_KEYS /usr/src/app/src/utils/clientConfig.js

# standard install/build commands
RUN npm install && npm run build

FROM dictybase/static-server:2.0.0
RUN mkdir /www
WORKDIR /www
COPY --from=0 /usr/src/app/build ./
ENTRYPOINT ["/usr/local/bin/app", "run", "-f", "/www"]
