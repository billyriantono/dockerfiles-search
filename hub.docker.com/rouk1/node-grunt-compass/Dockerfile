FROM node

RUN apt-get update -qq
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    ruby-full \
    locales \
    libssl-dev \
    ssh \
    wget \
    rsync \
    curl \
    git-all \
    unzip

# tools
RUN gem install --no-rdoc --no-ri sass -v 3.4.22
RUN gem install --no-rdoc --no-ri compass
RUN npm install -g grunt-cli gulp-cli bower

# Cleaning
RUN apt-get clean