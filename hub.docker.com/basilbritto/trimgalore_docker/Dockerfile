FROM ummidock/fastqc:0.11.7-1

MAINTAINER Basil Britto <basilbritto.xavier@uantwerpen.be>
RUN apt update && apt-get -y install python3-pip curl
RUN pip3 install --upgrade cutadapt

# Install Trim Galore
RUN curl -fsSL https://github.com/FelixKrueger/TrimGalore/archive/0.4.5.tar.gz -o trim_galore.tar.gz
RUN tar xvzf trim_galore.tar.gz

ENV PATH="/NGStools/TrimGalore-0.4.5/:$PATH"