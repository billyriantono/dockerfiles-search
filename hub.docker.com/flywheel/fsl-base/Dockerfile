FROM neurodebian:trusty
MAINTAINER Flywheel <support@flywheel.io>


# Install dependencies
RUN echo deb http://neurodeb.pirsquared.org data main contrib non-free >> /etc/apt/sources.list.d/neurodebian.sources.list
RUN echo deb http://neurodeb.pirsquared.org trusty main contrib non-free >> /etc/apt/sources.list.d/neurodebian.sources.list
RUN apt-get update \
    && apt-get install -y \
        bc \
        bsdtar \
        curl \
        fsl-5.0-complete \
        jq \
        lsb-core \
        python-pip \
        python3-pip \
        zip

# Make directory for flywheel spec (v0)
ENV FLYWHEEL=/flywheel/v0
RUN mkdir -p ${FLYWHEEL}

# Set ENV variables
ENV FSLBROWSER=/etc/alternatives/x-www-browser
ENV FSLDIR=/usr/share/fsl/5.0
ENV FSLMULTIFILEQUIT=TRUE
ENV FSLOUTPUTTYPE=NIFTI_GZ
ENV FSLTCLSH=/usr/bin/tclsh
ENV FSLWISH=/usr/bin/wish
ENV LD_LIBRARY_PATH=/usr/lib/fsl/5.0
ENV PATH=/usr/lib/fsl/5.0:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV POSSUMDIR=/usr/share/fsl/5.0

# Save docker env to json
RUN python -c 'import os, json; f=open("/tmp/gear_environ.json", "w"); json.dump(dict(os.environ), f)'
