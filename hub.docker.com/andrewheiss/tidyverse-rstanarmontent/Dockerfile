FROM node:10
LABEL maintainer="Andres Arango Heredia <aarangoh@everis.com>"

# Install Ruby
RUN apt-get update && \
    apt-get -y install ruby-full

# Disable SSL
RUN npm config set strict-ssl false --global
RUN npm config set registry http://registry.npmjs.org/ --global

# Install Yeoman and gulp globally
RUN npm install -g yo gulp@3.9.1

# Install the Liferay Theme Generator
RUN npm install -g generator-liferay-theme@^7.x.x

# Set custom config to Gem
RUN gem sources -r https://rubygems.org/ 
RUN echo '---\n:backtrace: false\n:bulk_threshold: 1000\n:sources:\n- http://rubygems.org\n:update_sources: true\n:verbose: true' > /root/.gemrc

# Install Ruby Sass and Compass
RUN gem install sass -v "=3.4.0"
RUN gem install compass

# Install the Ruby Sass middleware
RUN npm install -g gulp-ruby-sass

# Create volume for themes
RUN mkdir /root/liferay-themes
VOLUME /root/liferay-themes
