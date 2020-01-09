FROM eclipse/stack-base:ubuntu
User root
# Update aptitude with new repo
RUN apt-get update


# Install Chef
RUN apt-get -y install curl build-essential libxml2-dev libxslt-dev git
RUN curl -L https://www.opscode.com/chef/install.sh | bash

COPY ./chef-solo /home/user/chef-solo

# Make Chef available as a volume
VOLUME /opt/chef
