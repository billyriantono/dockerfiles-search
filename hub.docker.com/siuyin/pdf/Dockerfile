FROM ubuntu
RUN apt-get update && apt-get install -y \
	texlive-extra-utils \
	&& rm -rf /var/lib/apt/lists/*
COPY *.sh /usr/local/bin/
CMD ["bash"]
