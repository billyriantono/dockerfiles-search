# docker build -t bobbywlindsey/docker-jekyll .

# reference: https://hub.docker.com/_/ubuntu/
FROM ubuntu:16.04

# Adds metadata to the image as a key value pair example LABEL version="1.0"
LABEL maintainer="Bobby Lindsey <me@bobbywlindsey.com>"

# Set environment variables
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

# Create empty directory to attach volume
RUN mkdir ~/bobbywlindsey

# Install packages for building Ruby
RUN apt-get update
RUN apt-get remove ruby -y
RUN apt-get install wget -y
RUN apt-get install curl -y
RUN apt-get install git-core -y
RUN apt-get install build-essential -y
RUN apt-get install zlib1g-dev libssl-dev libreadline-dev libyaml-dev libxml2-dev libxslt-dev -y

# Clean up
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*

# Install rbenv
RUN git clone https://github.com/rbenv/rbenv.git ~/.rbenv
RUN git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
RUN echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
RUN echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
RUN echo 'eval "$(rbenv init -)"' >> ~/.bashrc
RUN echo 'eval "$(rbenv init -)"' >> /etc/profile.d/rbenv.sh
ENV PATH /root/.rbenv/bin:$PATH

# Install Ruby
RUN rbenv install 2.5.1
RUN rbenv global 2.5.1

# Disable generating local documentation for gems
RUN echo "gem: --no-document" > ~/.gemrc

# Install Jekyll
RUN /bin/sh -l -c "gem update"
RUN /bin/sh -l -c "gem install jekyll bundler"

# Add Jekyll-related bash functions to .bashrc
RUN echo "\
push-site() {\n\
    rsync -v -rz -e ssh --checksum --delete /root/bobbywlindsey/_site/ \$1@bobbywlindsey.com:public_html\n\
}\n\
\n\
build-prod-site() {\n\
    cd ~/bobbywlindsey;\n\
    JEKYLL_ENV=production bundle exec jekyll build --config _config.yml;\n\
}\n\
\n\
build-dev-site() {\n\
    cd ~/bobbywlindsey;\n\
    bundle exec jekyll serve --livereload --host 0.0.0.0 --drafts --config _config.yml,_config.docker.yml --force-polling;\n\
}" >> ~/.bashrc

# Bundle install gems
COPY Gemfile* /tmp/
WORKDIR /tmp
RUN /bin/sh -l -c "bundle install"

# Start in bash
WORKDIR /root/bobbywlindsey
ENTRYPOINT ["/bin/bash"]
