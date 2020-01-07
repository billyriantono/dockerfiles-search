# FROM alpine:edge
FROM alpine:3.4
MAINTAINER jgilley@chegg.com

# if edge libraries are needed use the following:
# RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories

# install base packages - BASH should only be used for debugging, it's almost a meg in size
# install ca-certificates
# clean up the apk cache (no-cache still caches the indexes)
# update the ca-certificates
RUN	apk --update --no-cache \
	add bash ca-certificates supervisor && \
	rm -rf /var/cache/apk/* && \
	update-ca-certificates

# Add the container config files
COPY container_confs /

# set our environment
ENV APP_ENV='DEVELOPMENT'
# ENV APP_ENV='PRODUCTION'

# create the supervisor run dir
# make sure that entrypoint and other scripts are executeable 
RUN mkdir -p /run/supervisord && \
	mv /etc/profile.d/color_prompt /etc/profile.d/color_prompt.sh && \
	chmod +x /entrypoint.sh /wait-for-it.sh /etc/profile /etc/profile.d/*.sh

# the entry point definition
ENTRYPOINT ["/entrypoint.sh"]

# default command for entrypoint.sh
CMD ["supervisor"]
