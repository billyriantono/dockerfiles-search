FROM bluelightltd/nginx-nodejs-v8:latest

RUN mv /usr/share/nginx/html /usr/share/nginx/html-orig

# Install global tools
RUN npm install --global @angular/cli@latest && npm install -g yarn && npm install -g gulp-cli