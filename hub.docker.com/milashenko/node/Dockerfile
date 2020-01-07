FROM    node:0.12.0

# Install app dependencies
RUN useradd -ms /bin/bash node && npm install -g bower && npm install -g grunt

USER node

CMD ["bash"]
