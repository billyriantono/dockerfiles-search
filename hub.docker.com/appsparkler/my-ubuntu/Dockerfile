FROM ubuntu:latest

# UPDATE apt & apt-get
RUN apt-get update && apt-get -y upgrade

# Jekyll Setup as per https://jekyllrb.com/docs/installation/ubuntu/
RUN /bin/bash
RUN apt-get install -y ruby-full build-essential zlib1g-dev
# It is best to avoid installing Ruby Gems as the root user. Therefore, we need to set up a gem installation directory for your user account. The following commands will add environment variables to your ~/.bashrc file to configure the gem installation path. Run them now:
RUN echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
RUn echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
RUN echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
RUN . ~/.bashrc
RUN gem install jekyll bundler
