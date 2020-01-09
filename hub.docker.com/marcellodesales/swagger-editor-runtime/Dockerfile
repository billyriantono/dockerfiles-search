FROM marcellodesales/nodejs-ruby
MAINTAINER Marcello_deSales@intuit.com

RUN mkdir /runtime
WORKDIR /runtime

# copy the contents from the current app directory during builds
ONBUILD ADD . /runtime

# Install all the dependencies from the application at once
RUN npm install -g bower && \
    npm install -g grunt-cli && \
    npm install -g node-compass && \
    gem install compass

# Run grunt serve
CMD ["grunt", "serve"]
