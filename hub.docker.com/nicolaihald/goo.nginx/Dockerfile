# Pull in the from the official nginx image.
FROM nginx:1.9

# Optionally set a maintainer name to let people know who made this image.
MAINTAINER Nicolai Hald <haldcph@gmail.com>


###############################################################################
#                                INSTALLATION
###############################################################################

# We'll need curl within the nginx image.
RUN apt-get update && apt-get install -y --no-install-recommends curl \
	 && apt-get clean \
	 && rm -rf /var/lib/apt/lists/*

###############################################################################
#                                CONFIGURATION
###############################################################################

### tweak nginx image set-up

# remove log symlinks
RUN rm /var/log/nginx/access.log /var/log/nginx/error.log

# Delete the default welcome to nginx page.
RUN rm /usr/share/nginx/html/*


###############################################################################
#                                    DATA
###############################################################################

COPY root/ /
RUN chmod +x /docker-entrypoint.sh



###############################################################################
#                                    START
###############################################################################

# Allow us to customize the entrypoint of the image.
ENTRYPOINT ["/docker-entrypoint.sh"]

# Start nginx in the foreground to play nicely with Docker.
CMD ["nginx", "-g", "daemon off;"]
