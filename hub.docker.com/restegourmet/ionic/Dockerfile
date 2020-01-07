FROM node:10.15.1-jessie

# Install ionic
RUN npm install -g ionic@4.12.0

# Install Cordova
RUN npm install -g cordova@8.1.2

# Install local web server
RUN npm install -g local-web-server@2.6.1

# Make angular cli available
RUN ln -s /app/node_modules/\@angular/cli/bin/ng /usr/bin