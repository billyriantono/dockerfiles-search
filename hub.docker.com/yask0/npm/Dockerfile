FROM yask0/nodejs:5.6.0

RUN \
apk --no-cache add curl && \
curl -LSs https://github.com/npm/npm/archive/v3.6.0.tar.gz | tar xz && \
cd npm-3.6.0 && \
echo "prefix=/usr" > npmrc && \
node cli.js install -gf && \
cd / && \
apk del curl && \
rm -rf /npm-3.6.0 \
	/usr/share/man \
	/usr/lib/node_modules/npm/Makefile \
	/usr/lib/node_modules/npm/changelogs \
	/usr/lib/node_modules/npm/configure \
	/usr/lib/node_modules/npm/doc \
	/usr/lib/node_modules/npm/html \
	/usr/lib/node_modules/npm/make.bat \
	/usr/lib/node_modules/npm/scripts \
	/usr/lib/node_modules/npm/test
