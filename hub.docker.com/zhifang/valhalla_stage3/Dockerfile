FROM zhifang/valhalla_stage2

# Install latest R
ENV R_LIBS=/opt/r
RUN echo '\n# r mirror' | tee -a /etc/apt/sources.list && \
    echo "\ndeb https://cloud.r-project.org/bin/linux/ubuntu xenial-cran35/" | tee -a /etc/apt/sources.list && \
    apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9 && \
    apt-get update -yq && \
    apt-get install -yq r-base r-base-core r-base-dev \
                        texlive-base texlive-latex-base texlive-generic-recommended \
                        texlive-fonts-recommended texlive-fonts-extra texlive-extra-utils texlive-latex-recommended \
                        texlive-latex-extra

# Install RStudio
RUN R_VERSION=$(wget --no-check-certificate -qO- https://s3.amazonaws.com/rstudio-desktop/current.ver) && \
    #wget -q https://download1.rstudio.org/rstudio-xenial-${R_VERSION}-amd64.deb && \
    #gdebi -n rstudio-xenial-${R_VERSION}-amd64.deb && \
    #rm rstudio-xenial-${R_VERSION}-amd64.deb
    wget -q https://s3.amazonaws.com/rstudio-ide-build/desktop/xenial/amd64/rstudio-1.2.1327-amd64.deb && \
    gdebi -n rstudio-1.2.1327-amd64.deb && \
    rm rstudio-1.2.1327-amd64.deb

# Install RStudio Server
RUN R_VERSION=$(wget --no-check-certificate -qO- https://s3.amazonaws.com/rstudio-server/current.ver) && \
    #wget -q http://download2.rstudio.org/rstudio-server-${R_VERSION}-amd64.deb && \
    #gdebi -n rstudio-server-${R_VERSION}-amd64.deb && \
    #rm rstudio-server-${R_VERSION}-amd64.deb && \
    wget -q https://s3.amazonaws.com/rstudio-ide-build/server/trusty/amd64/rstudio-server-1.2.1226-amd64.deb && \
    gdebi -n rstudio-server-1.2.1226-amd64.deb && \
    rm rstudio-server-1.2.1226-amd64.deb && \
    wget -q https://raw.githubusercontent.com/ZhifangYe/valhalla/master/helper/pam_help.sh && \
    mv pam_help.sh /usr/lib/rstudio-server/bin/pam_help && \
    printf "www-port=8486\n" >> /etc/rstudio/rserver.conf && \
    printf "rsession-which-r=/usr/bin/R\n" >> /etc/rstudio/rserver.conf && \
    printf "server-app-armor-enabled=0\n" >> /etc/rstudio/rserver.conf && \
    printf "r-libs-user=/opt/r\n" >> /etc/rstudio/rsession.conf && \
    printf "session-timeout-minutes=0\n" >> /etc/rstudio/rsession.conf && \
    cp /usr/lib/rstudio-server/extras/systemd/rstudio-server.service /lib/systemd/system/ && \
    systemctl enable rstudio-server

# Install AFNI
ENV PATH=/opt/afni:${PATH}
RUN export PATH=/opt/afni:${PATH} && \
    curl -sO https://afni.nimh.nih.gov/pub/dist/bin/linux_fedora_21_64/@update.afni.binaries && \
    tcsh /@update.afni.binaries -package linux_ubuntu_16_64 -bindir /opt/afni -apsearch yes -curl && \
    rm @update.afni.binaries

# Installing ANTs 2.3.1
ENV ANTSPATH=/opt/ants/
ENV PATH=${ANTSPATH}:${PATH}
RUN mkdir -p /opt/ants && \ 
    curl -sSL https://www.dropbox.com/s/tru40t1r5q02vyb/ANTs-ubuntu1604-v2.3.1-6f403d7.tar.gz | tar -xzC /opt/ants --strip-components 1

# ASHS v2.0.0 20180815 beta
ENV ASHS_ROOT=/opt/ashs
ENV PATH=/opt/ashs/bin:${PATH}
RUN wget -q https://www.dropbox.com/s/y8s24y0qoqpjqsi/ashs-fastashs_2.0.0_beta_20180815.zip && \
    unzip -q -o -d /opt ashs-fastashs_2.0.0_beta_20180815.zip && \
    rm ashs-fastashs_2.0.0_beta_20180815.zip && \
    mv /opt/ashs-fastashs_beta /opt/ashs
    
# C3D v1.1.0 (from OSF)
ENV PATH=/opt/c3d/bin:${PATH}
RUN mkdir /opt/c3d && \
    curl -sSL https://www.dropbox.com/s/e0duyba8r2sinqg/c3d-1.1.0-Linux-x86_64.tar.gz \
    | tar -xzC /opt/c3d --strip-components 1

# Dcm2niix v1.0.20181125
ENV PATH=/opt/dcm2niix:${PATH}
RUN wget -q https://github.com/rordenlab/dcm2niix/releases/download/v1.0.20181125/dcm2niix_25-Nov-2018_lnx.zip && \
    unzip -q -o -d /opt/dcm2niix dcm2niix_25-Nov-2018_lnx.zip && \
    rm dcm2niix_25-Nov-2018_lnx.zip

# PALM v112-alpha
ENV PATH=/opt/palm:${PATH}
RUN mkdir /opt/palm && \
    curl -sSL https://s3-us-west-2.amazonaws.com/andersonwinkler/palm/palm-alpha112.tar.gz \
    | tar -xzC /opt/palm --strip-components 1

# FSL_FIX v1.067 beta
ENV FIXVERSION=1.06 \
    FSL_FIX_OS=Linux \
    FSL_FIX_ARCH=x86_64 \
    FSL_FIXDIR=/opt/fsl_fix \
    FSL_FIX_OCTAVE=/usr/bin/octave \
    FSL_FIX_OCOPTS="--traditional -q --no-window-system" \
    FSL_FIX_OCEVAL="--eval" \
    FSL_FIX_MATLAB_MODE=2 \
    FSL_FIX_WBC=/opt/workbench/bin_linux64/wb_command \
    FSL_FIX_FSLMATLAB=${FSLDIR}/etc/matlab
ENV PATH=/opt/fsl_fix:${PATH}
RUN mkdir /opt/fsl_fix && \
    curl -sSL https://www.dropbox.com/s/fwd1t0xk0jfis0e/fix_v1.067.tar.gz | tar -xzC /opt/fsl_fix --strip-components 1 && \
    sed -i 's/FSL_FIX_MATLAB_ROOT=\/opt\/fmrib\/matlab/FSL_FIX_MATLAB_ROOT=\/opt\/matlab\//' /opt/fsl_fix/settings.sh && \
    sed -i 's/FSL_FIX_MATLAB_MODE=1/FSL_FIX_MATLAB_MODE=2/' /opt/fsl_fix/settings.sh && \
    sed -i 's/FSL_FIX_WBC=\/vols\/Data\/HCP\/workbench\/bin_linux64\/wb_command/FSL_FIX_WBC=\/opt\/workbench\/bin_linux64\/wb_command/' /opt/fsl_fix/settings.sh

# ICA_AROMA v0.4.4-beta
ENV PATH=/opt/ica_aroma:${PATH}
RUN mkdir /opt/ica_aroma && \
    curl -sSL https://github.com/maartenmennes/ICA-AROMA/archive/v0.4.4-beta.tar.gz \
    | tar -xzC /opt/ica_aroma --strip-components 1 && \
    chmod +x /opt/ica_aroma/ICA_AROMA.py

# ITK-SNAP v3.8.0 beta
ENV PATH=/opt/itksnap/bin:${PATH}
RUN mkdir -p /opt/itksnap && \
    curl -sSL https://www.dropbox.com/s/bjhqq33cuif88hk/itksnap-3.8.0-beta-20181028-Linux-x86_64.tar.gz \
    | tar -xzC /opt/itksnap --strip-components 1

# HCP WorkBench v1.3.2
ENV PATH=/opt/workbench/bin_linux64:${PATH}
RUN wget -q https://ftp.humanconnectome.org/workbench/workbench-linux64-v1.3.2.zip && \
    unzip -q -o -d /opt workbench-linux64-v1.3.2.zip && \
    rm workbench-linux64-v1.3.2.zip

# MRIcroGL v1.0.20181111
ENV PATH=/opt/mricrogl:${PATH}
RUN wget -q https://github.com/neurolabusc/MRIcroGL/releases/download/v1.0.20181111/MRIcroGL_linux.zip && \
    unzip -q -o -d /opt MRIcroGL_linux.zip && \
    rm MRIcroGL_linux.zip && \
    mv /opt/MRIcroGL /opt/mricrogl && \
    chmod 755 -R /opt/mricrogl && \
    rm /opt/mricrogl/dcm2niix

# SurfIce v1.0.20181114
ENV PATH=/opt/surfice:${PATH}
RUN wget -q https://github.com/neurolabusc/surf-ice/releases/download/v1.0.20181114/surfice_linux.zip && \
    unzip -q -o -d /opt surfice_linux.zip && \
    rm surfice_linux.zip && \
    mv /opt/Surf_Ice /opt/surfice && \
    chmod 755 -R /opt/surfice