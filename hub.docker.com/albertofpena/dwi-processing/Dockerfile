# This Dockerfile was based off: https://github.com/nipy/workshops/blob/master/170327-nipype/docker

FROM debian:buster
MAINTAINER Alberto Fernandez Pena <afernandez@hggm.es>

#---------------------------------------------
# Update OS dependencies and setup debian
#---------------------------------------------
USER root
RUN apt-get update -qq && apt-get install -yq --no-install-recommends \
						bzip2 \
						awscli \
                                                ca-certificates \
						dpkg-dev \
						git \
						g++ \
						libeigen3-dev \
						zlib1g-dev \
						libqt4-opengl-dev \
						libgl1-mesa-dev \
						libfftw3-dev \
						libtiff5-dev \
						tcsh \
						file \
						python \
						python-numpy \
						sudo \
                                                curl \
                                                tree \
                                                unzip \
                                                wget \
                                                xvfb \
                                                zip \
                                                vim \
                                                less && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
    
ENV DEBIAN_FRONTEND=noninteractive
RUN adduser --disabled-password --gecos '' docker && adduser docker sudo
RUN echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

#-----------------------------------
# Install FSL 6.0
#-----------------------------------
USER root
RUN mv /etc/debian_version /etc/debian_version.bak
RUN echo 9 > /etc/debian_version

USER docker
RUN wget https://fsl.fmrib.ox.ac.uk/fsldownloads/fslinstaller.py -O /home/docker/fslinstaller.py
RUN sudo python ~/fslinstaller.py -d /usr/local/fsl

USER root
RUN mv /etc/debian_version.bak /etc/debian_version

#-------------------
# Install FreeSurfer
#-------------------
USER root
RUN curl -sSL https://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/6.0.0/freesurfer-Linux-centos6_x86_64-stable-pub-v6.0.0.tar.gz | tar zx -C /opt \
    --exclude='freesurfer/trctrain' \
    --exclude='freesurfer/subjects/fsaverage_sym' \
    --exclude='freesurfer/subjects/fsaverage3' \
    --exclude='freesurfer/subjects/fsaverage4' \
    --exclude='freesurfer/subjects/fsaverage5' \
    --exclude='freesurfer/subjects/fsaverage6' \
    --exclude='freesurfer/subjects/cvs_avg35' \
    --exclude='freesurfer/subjects/cvs_avg35_inMNI152' \
    --exclude='freesurfer/subjects/bert' \
    --exclude='freesurfer/subjects/V1_average' \
    --exclude='freesurfer/average/mult-comp-cor' \
    --exclude='freesurfer/lib/cuda' \
    --exclude='freesurfer/lib/qt' && \
    ( echo "cHJpbnRmICJrcnp5c3p0b2YuZ29yZ29sZXdza2lAZ21haWwuY29tXG41MTcyXG4gKkN2dW12RVYzelRmZ1xuRlM1Si8yYzFhZ2c0RVxuIiA+IC9vcHQvZnJlZXN1cmZlci9saWNlbnNlLnR4dAo=" | base64 -d | sh )

ENV OS=Linux \
    FS_OVERRIDE=0 \
    FIX_VERTEX_AREA= \
    FSF_OUTPUT_FORMAT=nii.gz \
    FREESURFER_HOME=/opt/freesurfer
ENV SUBJECTS_DIR=$FREESURFER_HOME/subjects \
    FUNCTIONALS_DIR=$FREESURFER_HOME/sessions \
    MNI_DIR=$FREESURFER_HOME/mni \
    LOCAL_DIR=$FREESURFER_HOME/local \
    FSFAST_HOME=$FREESURFER_HOME/fsfast \
    MINC_BIN_DIR=$FREESURFER_HOME/mni/bin \
    MINC_LIB_DIR=$FREESURFER_HOME/mni/lib \
    MNI_DATAPATH=$FREESURFER_HOME/mni/data \
    FMRI_ANALYSIS_DIR=$FREESURFER_HOME/fsfast
ENV PERL5LIB=$MINC_LIB_DIR/perl5/5.8.5 \
    MNI_PERL5LIB=$MINC_LIB_DIR/perl5/5.8.5 \
    PATH=$FREESURFER_HOME/bin:$FSFAST_HOME/bin:$FREESURFER_HOME/tktools:$MINC_BIN_DIR:$PATH
    
#--------------------
# Install MRtrix3
#--------------------
USER docker
RUN git clone https://github.com/MRtrix3/mrtrix3.git /home/docker/mrtrix3
RUN cd /home/docker/mrtrix3 && ./configure && ./build
RUN /home/docker/mrtrix3/set_path

    
#----------------------------------------
# Clear apt cache and other empty folders
#----------------------------------------
USER root
RUN apt-get clean && apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /boot /media /mnt /srv && \
chmod a+w /tmp

USER docker
RUN mkdir -p /home/docker/work
WORKDIR /home/docker/work

CMD /bin/bash
