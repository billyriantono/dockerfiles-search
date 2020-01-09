FROM ubuntu:xenial

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -qq && apt-get install -yq --no-install-recommends \
    apt-utils \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && chmod 777 /opt && chmod a+s /opt

RUN apt-get update -qq && apt-get install -yq --no-install-recommends \
    apt-utils ca-certificates unzip xorg wget xvfb \
    bc libgomp1 libxmu6 libxt6 tcsh tar \
    ghostscript libgs-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && chmod 777 /opt && chmod a+s /opt

# Install packages required by dax
RUN apt-get update && apt-get install -yq --no-install-recommends \
    python-pip libfreetype6-dev pkg-config libxml2-dev libxslt1-dev \
    python-dev zlib1g-dev python-numpy python-scipy python-requests \
    python-urllib3 python-pandas python-tk python-seaborn python-setuptools \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && chmod 777 /opt && chmod a+s /opt

# Install dax 
RUN pip install dax==0.8.0

# Install MATLAB MCR in /opt/mcr/
ENV MCR_INHIBIT_CTF_LOCK 1
RUN mkdir /opt/mcr_install && \
    mkdir /opt/mcr && \
    wget -P /opt/mcr_install \
    https://www.mathworks.com/supportfiles/downloads/R2017a/deployment_files/R2017a/installers/glnxa64/MCR_R2017a_glnxa64_installer.zip && \
    unzip -q /opt/mcr_install/MCR_R2017a_glnxa64_installer.zip -d /opt/mcr_install && \
    /opt/mcr_install/install -destinationFolder /opt/mcr -agreeToLicense yes -mode silent && \
    rm -rf /opt/mcr_install /tmp/*

# Install CONN Standalone in /opt/conn/
RUN wget -P /opt/ http://www.nitrc.org/frs/download.php/10081/conn17f_glnxa64.zip && \
    unzip -qj /opt/conn17f_glnxa64.zip -d /opt/conn && \
    rm -f /opt/conn17f_glnxa64.zip

# Install src
COPY src /opt/src/

# Make bind points for I/O
RUN mkdir /INPUTS /OUTPUTS

# Get the spider
COPY spider.py /opt/spider.py
ENTRYPOINT ["python", "/opt/spider.py"]
