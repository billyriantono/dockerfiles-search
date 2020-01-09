FROM efec/git:2.7.4

LABEL maintainer="efec/node Docker Maintainers <li.jun.kuma@gmail.com>"

# Install node
RUN wget -O- https://deb.nodesource.com/setup_6.x | bash && \
    apt-get install -y nodejs && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
    
# Define default command.
CMD ["/bin/bash"]