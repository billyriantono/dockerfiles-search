FROM nginx:latest
MAINTAINER Thomas Bracher "thomas.bracher@cpe.fr"

RUN find / -perm +6000 -type f -exec chmod a-s {} \; || true
