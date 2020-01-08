#FROM centos/python-36-centos7:latest
#FROM rootproject/root-centos:latest
FROM centos:centos7

USER root

COPY . /tmp/src

RUN rm -rf /tmp/src/.git* && \
    chown -R 1001 /tmp/src && \
    chgrp -R 0 /tmp/src && \
    chmod -R g+w /tmp/src && \
    rm -rf /tmp/scripts && \
    mv /tmp/src/.s2i/bin /tmp/scripts

#RUN yum update

RUN yum install -y wget bzip2 git gcc gcc-c++ make httpd httpd-devel scl-utils centos-release-scl-rh 
RUN yum install -y rh-nodejs10

ENV PATH /opt/conda/bin:$PATH

RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-4.5.4-Linux-x86_64.sh -O /tmp/miniconda.sh && \
    chmod +x /tmp/miniconda.sh && \
    /bin/bash /tmp/miniconda.sh -b -p /opt/conda && \
    rm /tmp/miniconda.sh && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate jupyterlab" >> ~/.bashrc
    #/opt/conda/bin/conda clean -tipsy && \
    #conda update -n base conda

RUN mkdir .conda .cache .config .npm .local .jupyter /home/jupyternbs && \
    chown -R 1001:0 .conda .cache .config .npm .local .jupyter /home/jupyternbs && \
    chown -R 1001:0 /opt/conda && \
    mkdir -p /opt/app-root/etc /opt/app-root/bin && \
    chown -R 1001:0 /opt/app-root

USER 1001

ENV NPM_CONFIG_PREFIX=/opt/app-root \
    PYTHONPATH=/opt/app-root/src

LABEL io.k8s.description="S2I builder for custom Jupyter notebooks." \
      io.k8s.display-name="Jupyter Notebook" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,python,jupyter,jupyterhub" \
      io.openshift.s2i.scripts-url="image:///opt/app-root/builder"

RUN /tmp/scripts/assemble

CMD [ "/opt/app-root/builder/run" ]
