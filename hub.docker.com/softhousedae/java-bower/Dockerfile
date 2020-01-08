FROM softhousedae/java-node

RUN npm set progress=false

# Install Bower
# Includes workaround for https://github.com/npm/npm/issues/9863
RUN cd /usr/local/lib/ && mv ./node_modules ./node_modules.tmp && mv ./node_modules.tmp ./node_modules && npm install -g bower

RUN echo '{ "allow_root": true }' > /root/.bowerrc

