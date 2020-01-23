# This Dockerfile constructs a docker image to run ndmg ("Nutmeg")
#

# Start with the neurodata/ndmg 
FROM neurodata/ndmg_dev:staging
# neurodata/ndmg has python3.6 pip3.6 already installed.
# apt-get install -y zip unzip vim git curl libglu1 python-setuptools zlib1g-dev \
#    git libpng-dev libfreetype6-dev pkg-config g++ vim r-base-core libgsl0-dev build-essential \
#    openssl

# Note the Maintainer
MAINTAINER Flywheel <support@flywheel.io>

RUN apt-get update && \
	apt-get install -y \
	tree

# Install gear python dependencies
RUN pip3.6 install \
	flywheel_sdk \
	psutil && \
    rm -rf /root/.cache/pip && \
    rm -rf /var/lib/apt/lists/*


# Make directory for flywheel spec (v0)
ENV FLYWHEEL /flywheel/v0
WORKDIR ${FLYWHEEL}

# Copy and configure run script and metadata code
COPY run.py ${FLYWHEEL}/run.py
COPY manifest.json ${FLYWHEEL}/manifest.json
COPY utils ${FLYWHEEL}/utils
      

# Save docker environ
RUN python -c 'import os, json; f = open("/tmp/gear_environ.json", "w"); json.dump(dict(os.environ), f)'

# Configure entrypoint
RUN chmod a+x /flywheel/v0/run.py
ENTRYPOINT ["/flywheel/v0/run.py"]