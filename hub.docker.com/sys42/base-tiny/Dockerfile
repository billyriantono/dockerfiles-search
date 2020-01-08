###############################################################################
#
# Minimal base image with bash and curl in place
#
# Reasoning for the 5MB step in size:
#
#   (*) bash: will be our common scripting target. if speed or extreme small
#             memory footprint is required, we still can use the builtin shell
#
#   (*) curl: de-facto standard for accessing REST apis and fetch securely via
#             https. it pulls in ca-certificates and openssl, so security tools
#             are in place.
#
###############################################################################
FROM gliderlabs/alpine:3.2
MAINTAINER Tom Nussbaumer <thomas.nussbaumer@gmx.net>
RUN apk -U add bash curl && rm /var/cache/apk/*
