FROM python:3
MAINTAINER fjy8018@gmail.com

# should be covered
ENV TARGET_IP tyk_dashboard

COPY bootstrap.sh /

ENTRYPOINT ["/bin/bash", "-c", "/bootstrap.sh $TARGET_IP"]