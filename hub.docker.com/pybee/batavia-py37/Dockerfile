# Use the BeeWare Python image as a starting point.
FROM pybee/py37

# Copy the runtest script into the container
ADD tools /tools

# Install pytest and runners
RUN pip install pytest pytest-xdist pytest-runner pytest-tldr

# Add the node package source and install nodejs
RUN cd /tools && \
    apt-get install -y gnupg && \
    curl -sL https://deb.nodesource.com/setup_10.x -o nodesource_setup.sh && \
    chmod 755 nodesource_setup.sh && \
    ./nodesource_setup.sh && \
    apt-get install -y nodejs

# Install npm and the beefore javascript dependencies
RUN cd /tools && \
    npm install -g npm && \
    npm install -g

# Run the test with a waggle report
CMD ["/tools/run.sh"]
