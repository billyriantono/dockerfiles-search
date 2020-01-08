# create a file named Dockerfile
FROM node:argon

# Install necessary packages for compiling
RUN apt-get update -qq && apt-get install -y build-essential libssl-dev
RUN apt-get install -y ruby
RUN gem install sass

# Install yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb http://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -y yarn

# Make the folder to hold our app
RUN mkdir /app
WORKDIR /app

# Install gulp
RUN yarn global add gulp-cli
RUN yarn global add pm2

# Expose the ports
EXPOSE 8050
EXPOSE 35729

# Add the scripts
ADD ./run.sh /run.sh
RUN chmod 755 /*.sh

# Start the server
CMD ["/run.sh"]
