FROM ubuntu
RUN apt-get update && \
	apt-get install -y aptly
COPY root/ /
ENTRYPOINT ["entrypoint"]
CMD ["api", "serve"]
