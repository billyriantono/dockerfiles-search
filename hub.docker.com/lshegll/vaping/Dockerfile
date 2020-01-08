FROM python:3.6

RUN apt-get update \
	&& apt-get install -y \
		fping

# requirements for examples/standalone_dns/
RUN pip install \
	graphsrv \
	vodka \
	vaping

WORKDIR /opt/vaping

# The process just silently exits without --debug in docker.
CMD ["vaping", "--home=/opt/vaping/", "--verbose", "--debug", "start"]

EXPOSE 7021