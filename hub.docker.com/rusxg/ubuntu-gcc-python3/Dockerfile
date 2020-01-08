FROM ubuntu:16.04

RUN \
	apt-get update && \
	apt-get install build-essential python3 python3-pip -y && \
	pip3 install bitstring argparse && \
	apt-get -y clean all && \
	rm -rf /var/lib/apt/lists/*


