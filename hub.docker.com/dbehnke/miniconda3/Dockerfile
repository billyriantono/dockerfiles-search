FROM dbehnke/ol6:latest

RUN yum -y install wget bzip2 && \
    yum clean all && \
    rm -r -f /var/cache/* && rm -r -f /tmp/*
RUN echo 'export PATH=/opt/anaconda/bin:$PATH' > /etc/profile.d/conda.sh
RUN wget --quiet http://repo.continuum.io/miniconda/Miniconda3-3.7.0-Linux-x86_64.sh && \
    /bin/bash /Miniconda3-3.7.0-Linux-x86_64.sh -b -p /opt/anaconda && \
    rm Miniconda3-3.7.0-Linux-x86_64.sh && \
    source /etc/profile.d/conda.sh && \
    conda update --yes conda && \
    conda update --yes --all && \
    conda clean --yes --tarballs
   
CMD source /etc/profile.d/conda.sh && python $PYTHON_PARAMETERS

