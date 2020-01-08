# Debian: PHP5-CLI
#
# VERSION 0.0.1

# Pull the base image.
FROM ericmdev/essentials

# Set the author.
MAINTAINER Eric Mugerwa <dev@ericmugerwa.com>

# Set environment variables.
ENV FILES config/

# Install packages.
RUN apt-get update && apt-get install -y \
    php5-common \
    php5-cli

# Add managed php ini files.
ADD ${FILES}/etc/php5/cli/conf.d/cli.ini /etc/php5/cli/conf.d/

# Configure executable.
ENTRYPOINT ["/bin/bash"]

# Define default command.
CMD []