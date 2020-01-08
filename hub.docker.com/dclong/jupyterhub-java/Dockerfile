FROM dclong/jupyterhub-jdk:18.04_jdk11

ARG tmp_dir=/scripts/ijava
RUN mkdir $tmp_dir && cd $tmp_dir \
    && wget https://github.com/SpencerPark/IJava/releases/download/v1.2.0/ijava-1.2.0.zip -O ijava.zip \
    && unzip ijava.zip \
    && python3 install.py --sys-prefix \
    && cd /root \
    && rm -rf $tmp_dir
