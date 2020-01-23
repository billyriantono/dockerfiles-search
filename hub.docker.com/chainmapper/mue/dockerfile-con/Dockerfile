#################################################################
# Dockerfile
#
# Software Version:  maker2.31.10
# Description:      MAKER is a portable and easily configurable genome annotation pipeline.
# Code:             http://www.yandell-lab.org/software/maker.html
# Base Image:       conda/miniconda3
# Build Cmd:        sudo docker build -t cgwyx:maker .
# Pull Cmd:         docker pull cgwyx/canu
# Run Cmd:          sudo docker run -it --rm -v /home:/home --name=canu cgwyx/maker:latest /bin/bash
# File Author / Maintainer: cheng gong <512543469@qq.com>
#################################################################

FROM conda/miniconda2

RUN conda update --all -y &&\
    conda config --add channels conda-forge &&\
    conda config --add channels r &&\
    conda config --add channels bioconda &&\
    conda config --set show_channel_urls yes &&\
    conda install -y -c bioconda maker
    
CMD ["/bin/bash"]


