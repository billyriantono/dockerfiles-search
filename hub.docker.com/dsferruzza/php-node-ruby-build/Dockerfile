FROM dsferruzza/php-node-build
MAINTAINER David Sferruzza <david.sferruzza@gmail.com>

# Let the conatiner know that there is no tty
ENV DEBIAN_FRONTEND noninteractive

# Add Node.js repo
RUN apt-get update \
 && apt-get install --no-install-recommends -y \
 ruby \
 ruby-dev \
 bundler \
 libfreetype6 \
 libfontconfig \
 build-essential \
 # Slim down image
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/man/?? /usr/share/man/??_*

# Show versions
RUN node -v
RUN npm -v
RUN ruby -v
RUN bundle -v
RUN grunt --version
RUN bower --allow-root --version
