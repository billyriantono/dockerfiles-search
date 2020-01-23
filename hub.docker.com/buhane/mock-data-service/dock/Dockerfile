FROM ubuntu:trusty

RUN apt-get update && \
    apt-get install -y unzip xorg wget xvfb && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install packages required by dax
RUN apt-get update && apt-get install -y \
python-pip libfreetype6-dev pkg-config libxml2-dev libxslt1-dev \
python-dev zlib1g-dev python-numpy python-scipy python-requests \
python-urllib3 python-pandas
RUN pip install matplotlib --upgrade
RUN pip install pandas --upgrade
RUN pip install seaborn
RUN pip install pydicom==0.9.9

# Install dax 
RUN pip install https://github.com/VUIIS/dax/archive/v0.7.1.zip

# Install MATLAB MCR in /opt/mcr/
ENV MCR_INHIBIT_CTF_LOCK 1
ENV MAT_VER R2013a
ENV MCR_VER v81
RUN mkdir /opt/mcr_install && \
    mkdir /opt/mcr && \
    wget -q -P /opt/mcr_install \
    http://ssd.mathworks.com/supportfiles/MCR_Runtime/R2013a/MCR_R2013a_glnxa64_installer.zip && \
    unzip -q /opt/mcr_install/MCR_${MAT_VER}_glnxa64_installer.zip -d /opt/mcr_install && \
    /opt/mcr_install/install -destinationFolder /opt/mcr -agreeToLicense yes -mode silent && \
    rm -rf /opt/mcr_install /tmp/*

# Install SPM standalone with LST toolbox
RUN wget -q -P /opt/ \
    https://www.dropbox.com/s/ekstz5ho1i6lvzm/spm8-vbm8-LST1-Linux-2013a.zip && \
    unzip -q /opt/spm8-vbm8-LST1-Linux-2013a.zip -d /opt && \
    rm -f /opt/spm8-vbm8-LST1-Linux-2013a.zip && \
    /opt/spm_exec/run_spm8.sh /opt/mcr/v81 quit

# Initialize spm and then unset library path because it interferes with python
ENV SPM_DIR /opt/spm_exec
ENV SPM_EXEC ${SPM_DIR}/spm8
ENV LD_LIBRARY_PATH \
    /opt/mcr/${MCR_VER}/runtime/glnxa64:/opt/mcr/${MCR_VER}/bin/glnxa64:/opt/mcr/${MCR_VER}/sys/os/glnxa64:/opt/mcr/${MCR_VER}/sys/java/jre/glnxa64/jre/lib/amd64/native_threads:/opt/mcr/${MCR_VER}/sys/java/jre/glnxa64/jre/lib/amd64/server:/opt/mcr/${MCR_VER}/sys/java/jre/glnxa64/jre/lib/amd64/client:/opt/mcr/${MCR_VER}/sys/java/jre/glnxa64/jre/lib/amd64

ENV XAPPLRESDIR /opt/mcr/${MCR_VER}/X11/app-defaults
RUN chmod +x /opt/spm_exec/spm8
ENV LD_LIBRARY_PATH ""

# Install src
COPY src /opt/src/
RUN chmod +x /opt/src/run_script.sh

# Set permissions to avoid issues with Singularity
RUN chmod -R o+r /opt/

# Make mount points for I/O
RUN mkdir /INPUTS /OUTPUTS

# Get the spider code
COPY spider.py /opt/spider.py
ENTRYPOINT ["python", "/opt/spider.py"]
