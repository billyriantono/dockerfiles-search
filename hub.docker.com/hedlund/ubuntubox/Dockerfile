FROM ubuntu:xenial
MAINTAINER henrik@hedlund.im

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Set the timezone
RUN echo "Europe/Oslo" > /etc/timezone

# Install some tools that're nice to have down the line
RUN apt-get update && apt-get install -y curl git nano \
    && rm -rf /var/lib/apt/lists/*

# Set xterm so we can use nano and other editors
ENV TERM xterm

# Let's use bash instead of sh to make it simpler to install stuff
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Run bash as the default command, but avoid using an entrypoint to we
# can easily override it...
CMD ["/bin/bash"]
