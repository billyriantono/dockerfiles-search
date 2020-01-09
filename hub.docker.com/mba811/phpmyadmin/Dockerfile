FROM mba811/nginx-php:latest
MAINTAINER Tsong khapa <ztd811@yahoo.com>
ENV VERSION 4.4.2
CMD /bin/sh -c mkdir -p /data/http && \
	cd /data/http && \
	wget -O - "http://www.sourceforge.net/projects/phpmyadmin/files/phpMyAdmin/${VERSION}/phpMyAdmin-${VERSION}-all-languages.tar.gz/download" | tar --strip-components=1 -x -z && \
	rm -rf *.md .coveralls.yml ChangeLog composer.json config.sample.inc.php DCO doc examples phpunit.* README RELEASE-DATE-* setup
ADD data /data