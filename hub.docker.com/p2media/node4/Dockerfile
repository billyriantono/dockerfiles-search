FROM node:4

# `apt-get update` will fail because the repositories aren't available anymore!
# Thus we ignore the error by echo'ing something
RUN apt-get update || echo ""
RUN apt-get install -y fontforge ttfautohint
RUN npm install -g grunt-cli phantomjs node-sass@3.4.2
