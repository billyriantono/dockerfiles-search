FROM phusion/passenger-customizable:0.9.14

MAINTAINER Tahi Project Team <tahiprojectteam@plos.org>
# VERSION 0.0.1

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update -q

# Install git and build tools
RUN /build/utilities.sh
# Install Ruby
RUN /build/ruby2.1.sh
# Install Node
RUN /build/nodejs.sh

RUN echo "gem: --no-ri --no-rdoc" > /etc/gemrc

RUN mkdir -p /home/app/ihat && chown -R app /var/lib /usr/local/bin /home/

USER app
ENV HOME /home

WORKDIR /home/app/ihat

# Install base gems
RUN gem install rake bundler
ADD ./Gemfile /home/app/ihat/Gemfile
ADD ./Gemfile.lock /home/app/ihat/Gemfile.lock
RUN bundle pack --all
RUN bundle install --deployment

# Add all files from the project directory to the container
ADD . /home/app/ihat

USER root
RUN chown -R app /home/app/

# Mount the a volume at runtime to share files from the working directory
# on the host computer
# http://stackoverflow.com/questions/26145351/why-doesnt-chown-work-in-dockerfile
VOLUME /home/app/ihat


RUN /usr/bin/workaround-docker-2267
RUN mkdir -p /etc/my_init.d

# Use baseimage-docker's init process
CMD ["/sbin/my_init"]

# Use baseimage-docker's init process.
EXPOSE 3000

# Clean up APT when done
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
