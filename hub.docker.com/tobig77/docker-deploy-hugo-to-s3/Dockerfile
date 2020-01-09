FROM tobig77/docker-hugo

RUN \
	mkdir -p /aws && \
	apk -Uuv add groff less python py-pip git openssh-client tar gzip ca-certificates && \
  	pip install awscli && \
	apk --purge -v del py-pip && \
	rm /var/cache/apk/*
