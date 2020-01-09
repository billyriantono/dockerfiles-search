FROM ruby:2.5.5
ENV LANG C.UTF-8

# Fix for error in apt update
RUN printf "deb http://archive.debian.org/debian/ jessie main\ndeb-src http://archive.debian.org/debian/ jessie main\ndeb http://security.debian.org jessie/updates main\ndeb-src http://security.debian.org jessie/updates main" > /etc/apt/sources.list

# Install dependencies and sql client
RUN apt-get update && apt-get install -y nodejs \
    wget \
    default-libmysqlclient-dev

# Configure the main working directory. This is the base 
# directory used in any further RUN, COPY, and ENTRYPOINT 
# commands.
COPY ./application /ruby/src/app
WORKDIR /ruby/src/app

# Copy the Gemfile as well as the Gemfile.lock and install 
# the RubyGems. This is a separate step so the dependencies 
# will be cached unless changes to one of those two files 
# are made.
RUN gem install bundler && gem install mysql2 && bundle install --jobs 20 --retry 5

# Expose port 3000 to the Docker host, so we can access it 
# from the outside.
EXPOSE 3000

# The main command to run when the container starts. Also 
# tell the Rails dev server to bind to all interfaces by 
# default.
CMD ["sh", "-c", "rails db:migrate && rails server -b 0.0.0.0"]