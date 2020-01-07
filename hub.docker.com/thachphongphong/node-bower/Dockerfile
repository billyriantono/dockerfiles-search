# Pull base image.
FROM library/node:8
MAINTAINER Linh Do <truonglinhdo@gmail.com>

# Install Bower & Grunt
RUN npm install -g bower && \
    echo '{ "allow_root": true }' > /root/.bowerrc

# Define working directory.
WORKDIR /app

# Define default command.
CMD ["bash"]