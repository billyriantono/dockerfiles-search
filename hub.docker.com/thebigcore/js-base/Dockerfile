FROM node:latest

RUN npm config set cache /cache/npm --global && \
    npm install -g webpack@1.12.2 webpack-dev-server typescript tsd \
        bower babel babel-cli --no-bin-links --loglevel warn --no-color && \
    rm -rf /cache/*


