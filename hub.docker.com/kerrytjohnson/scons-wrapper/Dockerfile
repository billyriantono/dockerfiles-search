FROM centos:centos7.5.1804

RUN echo "[main]"                               >> /etc/yum/yum.conf    \
    && echo "skip_missing_names_on_install=0"   >> /etc/yum/yum.conf    \
    && echo "skip_missing_names_on_update=0"    >> /etc/yum/yum.conf

RUN yum -y -q install   python3     \  
                        python3-pip

RUN python3 -m pip install pyyaml scons

COPY / /usr/local/scons-wrapper
