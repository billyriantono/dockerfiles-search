FROM viur/viur-base
MAINTAINER http://www.viur.is
WORKDIR /src
ADD . .

ENV SDK_VERSION 1.9.34

RUN npm install -g less && \
	pip install "git+https://github.com/pyjs/pyjs.git#egg=pyjs" && \
	cd /src && curl -sL https://storage.googleapis.com/appengine-sdks/featured/google_appengine_${SDK_VERSION}.zip -o google_appengine_${SDK_VERSION}.zip && \
	unzip google_appengine_${SDK_VERSION}.zip &&  \
	rm google_appengine_${SDK_VERSION}.zip &&  \
	cp scripts/* /usr/bin/ && \
	chmod 755 /usr/bin/buildapp && \
	chmod 755 /usr/bin/startapp && \
	mkdir /Projects

VOLUME ["/Projects"]

EXPOSE 8000 8080
