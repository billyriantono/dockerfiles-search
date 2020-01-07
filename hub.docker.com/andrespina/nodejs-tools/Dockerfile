FROM node:9.2.0

MAINTAINER Andres Pina

# Install glup tool
RUN npm install -g gulp-cli gulp --silent

# Install Javascript linter
RUN npm install -g eslint@^4.11.0 --silent
RUN npm install -g --save eslint-plugin-import@^2.7.0 --silent && \
  npm install -g --save eslint-plugin-jsx-a11y@^6.0.2 --silent && \
  npm install -g --save eslint-plugin-react@^7.4.0 --silent
RUN npm install -g --save eslint-config-airbnb --silent

# Install sass linter
RUN npm install -g sass-lint --silent


