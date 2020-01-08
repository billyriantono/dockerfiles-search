#
# ruby-2.20 Dockerfile
#
# https://github.com/bcallencs/ruby-2.2.0
#

# Pull base image.
FROM bcallencs/rbenv
MAINTAINER Brad Allen <bcallencs@gmail.com>

# As the user Ruby
USER ruby

# Install ruby 2.2.0
RUN rbenv install 2.2.0
RUN rbenv global 2.2.0

CMD ["true"]