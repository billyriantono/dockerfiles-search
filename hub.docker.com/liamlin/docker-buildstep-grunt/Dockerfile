FROM        node
# 1. npm install global grunt bower
# 2. npm install && bower install
# 3. grunt build
RUN         npm install -g bower grunt-cli
WORKDIR     /usr/src/src/frontend
CMD         npm install && bower install && grunt build --force --output=/usr/src/portal/frontend/static/
