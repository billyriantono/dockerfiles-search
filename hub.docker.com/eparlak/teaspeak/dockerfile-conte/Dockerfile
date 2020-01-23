############################################################
# Dockerfile
############################################################

# Set the base image
FROM alpine:3.8

############################################################
# Configuration
############################################################
ENV VERSION "0.6.3"

############################################################
# Entrypoint
############################################################
COPY docker-entrypoint.sh /usr/local/bin/

############################################################
# Installation
############################################################

RUN apk --no-cache add bash curl &&\
    curl -L -o /usr/local/bin/kubectx https://raw.githubusercontent.com/ahmetb/kubectx/v${VERSION}/kubectx &&\
	curl -L -o /usr/local/bin/kubens https://raw.githubusercontent.com/ahmetb/kubectx/v${VERSION}/kubens &&\
    chmod +x /usr/local/bin/kubectx &&\
    chmod +x /usr/local/bin/kubens &&\
    chmod +x /usr/local/bin/docker-entrypoint.sh

############################################################
# Execution
############################################################
ENTRYPOINT [ "docker-entrypoint.sh" ]
CMD [ "kubectx", "--help"]
