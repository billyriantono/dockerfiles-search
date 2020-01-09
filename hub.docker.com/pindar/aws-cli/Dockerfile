FROM ubuntu:14.04

#
# Install amazon related tools
# ----------------------------

# install prerequisits
RUN apt-get -qq -y update && \
	apt-get install -y unzip python-setuptools wget && \
	apt-get install -y awscli

# Define working directory.
WORKDIR /data

CMD ["-"]
ENTRYPOINT ["aws"]