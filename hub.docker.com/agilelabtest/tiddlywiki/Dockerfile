FROM node:9.8.0-alpine

RUN npm install -g tiddlywiki@5.1.18

# Setup wiki volume
VOLUME /var/lib/tiddlywiki
WORKDIR /var/lib/tiddlywiki

# Install plugins
ADD plugins/TW5-HotZone/dist/felixhayashi/hotzone /usr/local/lib/node_modules/tiddlywiki/plugins/felixhayashi/hotzone
ADD plugins/TW5-Vis.js/dist/felixhayashi/vis /usr/local/lib/node_modules/tiddlywiki/plugins/felixhayashi/vis
ADD plugins/TW5-TopStoryView/dist/felixhayashi/topstoryview /usr/local/lib/node_modules/tiddlywiki/plugins/felixhayashi/topstoryview
ADD plugins/TW5-TiddlyMap/dist/felixhayashi/tiddlymap /usr/local/lib/node_modules/tiddlywiki/plugins/felixhayashi/tiddlymap

#ADD wiki /var/lib/tiddlywiki/wiki

ADD run-wiki.sh /usr/local/bin/run-wiki
CMD chmod +x /usr/local/bin/run-wiki

ADD init-wiki.sh /usr/local/bin/init-wiki
CMD chmod +x /usr/local/bin/init-wiki

ADD readonly-wiki.sh /usr/local/bin/readonly-wiki
CMD chmod +x /usr/local/bin/readonly-wiki

ADD write-wiki.sh /usr/local/bin/write-wiki
CMD chmod +x /usr/local/bin/write-wiki

#CMD ["/usr/local/bin/run-wiki.sh"]
