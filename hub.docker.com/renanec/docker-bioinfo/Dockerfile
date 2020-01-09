FROM rocker/verse:3.5.0

RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
	apt-get install -y python python3 python-dev python-pip python-virtualenv && \
	rm -rf /var/lib/apt/lists/*

RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
	perl

# Environment variables
# 150314 == plink 1.9 beta 3 ???
ENV PLINK_VERSION       180717
ENV PLINK_HOME          /usr/local/plink
ENV PATH                $PLINK_HOME:$PATH

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y unzip wget && \
    wget https://www.cog-genomics.org/static/bin/plink$PLINK_VERSION/plink_linux_x86_64.zip && \
    unzip plink_linux_x86_64.zip -d $PLINK_HOME && \
    rm plink_linux_x86_64.zip && \
    DEBIAN_FRONTEND=noninteractive apt-get autoremove -y unzip wget && \
    rm -rf /var/lib/apt/lists/*

ADD requirements.txt requirements.txt
RUN pip install -r requirements.txt

