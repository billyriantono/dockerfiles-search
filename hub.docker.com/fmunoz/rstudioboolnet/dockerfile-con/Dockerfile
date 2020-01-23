# Creates docker container that runs HCP Pipeline algorithms
#
#

# Use Ubuntu 16.04 LTS
FROM ubuntu:xenial

LABEL maintainer="Flywheel <support@flywheel.io>"

# Install all apt-get dependencies at once.
RUN apt-get update && \
    echo "\n\nInstalling FSL Requirements\n\n" && \
    apt-get install -y --no-install-recommends \
    software-properties-common \
    bc \
    bsdtar \
    curl \
    jq \
    lsb-core \
    python-pip \
    python3-pip \
    rename \
    wget \
    zip \
    unzip && \
    echo "\n\nInstalling FreeSurfer Requirements. \n\n" && \
    apt-get install -y --no-install-recommends \
    tcsh \
    tar \ 
    libgomp1 \
    perl-modules && \
    echo "\n\nInstalling gradient unwarp script requirements. \n\n" && \
    apt-get install -y --no-install-recommends \ 
    python-dev \
    python-numpy \
    python-scipy \
    python-nibabel \
    build-essential \
    autoconf \
    libtool && \
    echo "\n\nInstalling additional HCP-Pipeline dependencies. \n\n" && \
    apt-get install -y --no-install-recommends \
    libxmu6 \
    libxi6 \
    libxt6 \
    libx11-6 \
    libglu1-mesa \
    libfreetype6 \
    libblas3 \
    liblapack3 \
    zlib1g \
    python3-pip \
    gawk \
    zip \
    unzip \
    gzip && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

#############################################
# Download and install FSL 6.0.1 
# (see https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/FslInstallation/Linux)
# The installation script, fslinstaller.py, needs Python 2.7 to install.
# Leveraging del_fsl.txt reduces images size by 3 GB
COPY del_fsl.txt .
RUN wget -P /tmp/ https://fsl.fmrib.ox.ac.uk/fsldownloads/fslinstaller.py && \ 
    mkdir -p /usr/share/fsl/ && \ 
    python /tmp/fslinstaller.py -d /usr/share/fsl/6.0 -q && \
    cat del_fsl.txt | xargs rm -rf && \
    rm del_fsl.txt

# Configure FSL environment
ENV FSLDIR=/usr/share/fsl/6.0 \ 
    FSL_DIR="${FSLDIR}" \ 
    FSLOUTPUTTYPE=NIFTI_GZ \ 
    PATH=/usr/share/fsl/6.0/bin:$PATH \ 
    FSLMULTIFILEQUIT=TRUE \ 
    POSSUMDIR=/usr/share/fsl/6.0 \ 
    LD_LIBRARY_PATH=/usr/share/fsl/6.0/lib:$LD_LIBRARY_PATH \ 
    FSLTCLSH=/usr/bin/tclsh \ 
    FSLWISH=/usr/bin/wish

#############################################
# Download and install Connectome Workbench 1.3.2 
# Compatible with HCP v4.0.1
# https://www.humanconnectome.org/storage/app/media/workbench/workbench-linux64-v1.3.2.zip
# https://www.humanconnectome.org/storage/app/media/workbench/workbench-linux64-v1.4.1.zip
RUN cd /opt/ && \
    wget https://www.humanconnectome.org/storage/app/media/workbench/workbench-linux64-v1.4.2.zip -O workbench.zip && \
    unzip workbench.zip && \
    rm workbench.zip && \
    cd /

ENV CARET7DIR=/opt/workbench/bin_linux64

#############################################
# Download and install HCP Pipelines

# Using v4.0.1
RUN wget -nv https://github.com/Washington-University/HCPpipelines/archive/v4.0.1.tar.gz -O pipelines.tar.gz && \
    cd /opt/ && \
    tar zxvf /pipelines.tar.gz && \
    mv /opt/*ipelines* /opt/HCP-Pipelines && \
    rm /pipelines.tar.gz && \
    cd / 

# Set up specific environment variables for the HCP Pipeline
ENV FSL_DIR="${FSLDIR}" \ 
    HCPPIPEDIR=/opt/HCP-Pipelines \ 
    MSMBINDIR=${HCPPIPEDIR}/MSMBinaries \ 
    MSMCONFIGDIR=${HCPPIPEDIR}/MSMConfig
#ENV MATLAB_COMPILER_RUNTIME=/media/myelin/brainmappers/HardDrives/1TB/MATLAB_Runtime/v901
#ENV FSL_FIXDIR=/media/myelin/aahana/fix1.06

#For HCP Pipeline v4.0.1
ENV MSMBin=${HCPPIPEDIR}/MSMBinaries \
    HCPPIPEDIR_Templates=${HCPPIPEDIR}/global/templates \ 
    HCPPIPEDIR_Bin=${HCPPIPEDIR}/global/binaries \ 
    HCPPIPEDIR_Config=${HCPPIPEDIR}/global/config \ 
    HCPPIPEDIR_PreFS=${HCPPIPEDIR}/PreFreeSurfer/scripts \ 
    HCPPIPEDIR_FS=${HCPPIPEDIR}/FreeSurfer/scripts \ 
    HCPPIPEDIR_PostFS=${HCPPIPEDIR}/PostFreeSurfer/scripts \ 
    HCPPIPEDIR_fMRISurf=${HCPPIPEDIR}/fMRISurface/scripts \ 
    HCPPIPEDIR_fMRIVol=${HCPPIPEDIR}/fMRIVolume/scripts \ 
    HCPPIPEDIR_tfMRI=${HCPPIPEDIR}/tfMRI/scripts \ 
    HCPPIPEDIR_dMRI=${HCPPIPEDIR}/DiffusionPreprocessing/scripts \ 
    HCPPIPEDIR_dMRITract=${HCPPIPEDIR}/DiffusionTractography/scripts \ 
    HCPPIPEDIR_Global=${HCPPIPEDIR}/global/scripts \ 
    HCPPIPEDIR_tfMRIAnalysis=${HCPPIPEDIR}/TaskfMRIAnalysis/scripts

#try to reduce strangeness from locale and other environment settings
ENV LC_ALL=C \ 
    LANGUAGE=C
#POSIXLY_CORRECT currently gets set by many versions of fsl_sub, unfortunately, but at least don't pass it in if the user has it set in their usual environment
RUN unset POSIXLY_CORRECT

#############################################
# Download and install FreeSurfer
# 6.0.1 ftp://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/6.0.1/freesurfer-Linux-centos6_x86_64-stable-pub-v6.0.1.tar.gz
# 5.3.0 ftp://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/5.3.0-HCP/freesurfer-Linux-centos4_x86_64-stable-pub-v5.3.0-HCP.tar.gz
COPY del_freesurfer.txt .
RUN wget -nv -O- ftp://surfer.nmr.mgh.harvard.edu/pub/dist/freesurfer/6.0.1/freesurfer-Linux-centos6_x86_64-stable-pub-v6.0.1.tar.gz | tar zxv -C /opt \
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
    --exclude='freesurfer/lib/qt'  && \
    cat del_freesurfer.txt | xargs rm -rf && \
    rm del_freesurfer.txt


# Set up the FreeSurfer environment
ENV OS=Linux \ 
    FS_OVERRIDE=0 \ 
    FIX_VERTEX_AREA= \ 
    SUBJECTS_DIR=/opt/freesurfer/subjects \ 
    FSF_OUTPUT_FORMAT=nii.gz \ 
    MNI_DIR=/opt/freesurfer/mni \ 
    LOCAL_DIR=/opt/freesurfer/local \ 
    FREESURFER_HOME=/opt/freesurfer \ 
    FSFAST_HOME=/opt/freesurfer/fsfast \ 
    MINC_BIN_DIR=/opt/freesurfer/mni/bin \ 
    MINC_LIB_DIR=/opt/freesurfer/mni/lib \ 
    MNI_DATAPATH=/opt/freesurfer/mni/data \ 
    FMRI_ANALYSIS_DIR=/opt/freesurfer/fsfast \ 
    PERL5LIB=/opt/freesurfer/mni/lib/perl5/5.8.5 \ 
    MNI_PERL5LIB=/opt/freesurfer/mni/lib/perl5/5.8.5 \ 
    PATH=/opt/freesurfer/bin:/opt/freesurfer/fsfast/bin:/opt/freesurfer/tktools:/opt/freesurfer/mni/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:$PATH

#############################################
# Download and install gradient unwarp script
# note: python2.7 is needed for the fsl installer and the gradient unwarp 
# note: python3-dev needed for Ubuntu 14.04 (but not for 16.04)
# latest = v1.0.3
RUN wget -nv https://github.com/Washington-University/gradunwarp/archive/v1.0.3.tar.gz -O gradunwarp.tar.gz && \
    cd /opt/ && \
    tar zxvf /gradunwarp.tar.gz && \
    mv /opt/gradunwarp-* /opt/gradunwarp && \
    cd /opt/gradunwarp/ && \
    python setup.py install && \
    rm /gradunwarp.tar.gz && \
    cd / 

#############################################
# Download amnd install MSM_HOCR v3 binary
ENV MSMBINDIR=${HCPPIPEDIR}/MSMBinaries

RUN mkdir -p ${MSMBINDIR} && \
    wget -nv https://github.com/ecr05/MSM_HOCR/releases/download/1.0/msm_ubuntu -O ${MSMBINDIR}/msm && \
    chmod +x ${MSMBINDIR}/msm
#############################################

# Install PIP gear dependencies
COPY requirements.txt ${FLYWHEEL}/requirements.txt
RUN pip3 install --upgrade pip && \
    apt-get update && \
    apt-get remove -y python3-urllib3 && \
    pip3.5 install setuptools && \
    pip3.5 install -r requirements.txt && \
    rm -rf /root/.cache/pip

# Make directory for flywheel spec (v0)
ENV FLYWHEEL /flywheel/v0
WORKDIR ${FLYWHEEL}

# Copy suite packages to Gear
COPY utils ${FLYWHEEL}/utils

# Copy additional scripts and scenes
COPY scripts /tmp/scripts
COPY scenes /tmp/scenes
COPY scripts/patch/DiffPreprocPipeline.sh /opt/HCP-Pipelines/DiffusionPreprocessing/

# ENV preservation for Flywheel Engine
RUN python3 -c 'import os, json; f = open("/tmp/gear_environ.json", "w"); json.dump(dict(os.environ), f)'

# Configure entrypoint
ENTRYPOINT ["bash"]
