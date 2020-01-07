FROM docker:17.10-git

RUN apk -Uuv add groff less python py-pip jq gettext bash && \
	pip install awscli && \
	apk --purge -v del py-pip && \
	rm /var/cache/apk/*

CMD ["bash"]