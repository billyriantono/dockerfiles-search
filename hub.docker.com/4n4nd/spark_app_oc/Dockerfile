# This image provides a Python 3.6 environment you can use to run your Python
# applications.
FROM centos/s2i-base-centos7

EXPOSE 8080

ENV PYTHON_VERSION=3.6 \
    PATH=$HOME/.local/bin/:$PATH \
    PYTHONUNBUFFERED=1 \
    PYTHONIOENCODING=UTF-8 \
    LC_ALL=en_US.UTF-8 \
    LANG=en_US.UTF-8 \
    PIP_NO_CACHE_DIR=off

ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV PYTHONIOENCODING UTF-8
ENV CONDA_DIR /opt/conda
ENV NB_USER=nbuser
ENV NB_UID=1011
ENV NB_PYTHON_VER=3.6
ENV MINICONDA_VERSION=Miniconda3-latest-Linux-x86_64.sh

ENV SUMMARY="Platform for building and running Python $PYTHON_VERSION applications" \
    DESCRIPTION="Python $PYTHON_VERSION available as container is a base platform for \
building and running various Python $PYTHON_VERSION applications and frameworks. \
Python is an easy to learn, powerful programming language. It has efficient high-level \
data structures and a simple but effective approach to object-oriented programming. \
Python's elegant syntax and dynamic typing, together with its interpreted nature, \
make it an ideal language for scripting and rapid application development in many areas \
on most platforms."

LABEL summary="$SUMMARY" \
      description="$DESCRIPTION" \
      io.k8s.description="$DESCRIPTION" \
      io.k8s.display-name="Python 3.6" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,python,python36,rh-python36" \
      com.redhat.component="python36-container" \
      name="centos/python-36-centos7" \
      version="1" \
      usage="s2i build https://github.com/sclorg/s2i-python-container.git --context-dir=3.6/test/setup-test-app/ centos/python-36-centos7 python-sample-app" \
      maintainer="SoftwareCollections.org <sclorg@redhat.com>"

RUN INSTALL_PKGS="rh-python36 rh-python36-python-devel rh-python36-python-setuptools rh-python36-python-pip nss_wrapper \
        httpd24 httpd24-httpd-devel httpd24-mod_ssl httpd24-mod_auth_kerb httpd24-mod_ldap \
        httpd24-mod_session atlas-devel gcc-gfortran libffi-devel libtool-ltdl enchant" && \
    yum install -y centos-release-scl && \
    yum -y --setopt=tsflags=nodocs install --enablerepo=centosplus $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    # Remove centos-logos (httpd dependency) to keep image size smaller.
    rpm -e --nodeps centos-logos && \
    yum -y clean all --enablerepo='*'

RUN yum install -y curl wget java-headless bzip2 gnupg2 sqlite3 \
    && yum clean all -y \
    && cd /tmp \
    && wget -q https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh \
  #  && echo d0c7c71cc5659e54ab51f2005a8d96f3 $MINICONDA_VERSION | md5sum -c - \
    && bash Miniconda3-latest-Linux-x86_64.sh -b -p $CONDA_DIR \
    && rm Miniconda3-latest-Linux-x86_64.sh \
    && export PATH=/opt/conda/bin:$PATH \
    && yum install -y gcc gcc-c++ glibc-devel \
    && /opt/conda/bin/conda install --quiet --yes python=$NB_PYTHON_VER 'nomkl' \
			    'ipywidgets=5.2*' \
			    'matplotlib' \
			    'scipy' \
			    'seaborn' \
			    'cloudpickle' \
			    statsmodels \
			    pandas \
			    'dill' \
			    notebook \
			    jupyter \
          py4j \
          pyspark \
    && pip install pystan \
    && pip install widgetsnbextension fbprophet \
    && yum erase -y gcc gcc-c++ glibc-devel \
    && yum clean all -y \
    && rm -rf /root/.npm \
    && rm -rf /root/.cache \
    && rm -rf /root/.config \
    && rm -rf /root/.local \
    && rm -rf /root/tmp \
    && useradd -m -s /bin/bash -N -u $NB_UID $NB_USER \
    && usermod -g root $NB_USER \
    && chown -R $NB_USER $CONDA_DIR \
    # && conda remove --quiet --yes --force qt pyqt \
    && conda remove --quiet --yes --force --feature mkl ; conda clean -tipsy


# Copy the S2I scripts from the specific language image to $STI_SCRIPTS_PATH.
# COPY ./s2i/bin/ $STI_SCRIPTS_PATH
#
# # Copy extra files to the image.
# COPY ./root/ /
#
# # - Create a Python virtual environment for use by any application to avoid
# #   potential conflicts with Python packages preinstalled in the main Python
# #   installation.
# # - In order to drop the root user, we have to make some directories world
# #   writable as OpenShift default security model is to run the container
# #   under random UID.
# RUN source scl_source enable rh-python36 && \
#     virtualenv ${APP_ROOT} && \
#     chown -R 1001:0 ${APP_ROOT} && \
#     fix-permissions ${APP_ROOT} -P && \
#     rpm-file-permissions

ENV PATH /opt/conda/bin:$PATH

# ENV SPARK_HOME /opt/spark
RUN yum install -y  java-1.8.0-openjdk \
    && yum clean all && \
    rpm -q  java-1.8.0-openjdk

# Add all artifacts to the /tmp/artifacts
# directory
COPY \
    spark-2.3.0-bin-hadoop2.7.tgz \
    # oshinko_v0.5.3_linux_amd64.tar.gz \
    /tmp/artifacts/
# Add a notebook profile.

RUN mkdir /notebooks && chown $NB_UID:root /notebooks && chmod 1777 /notebooks

EXPOSE 8888

RUN mkdir -p -m 700 /home/$NB_USER/.jupyter/ && \
    echo "c.NotebookApp.ip = '*'" >> /home/$NB_USER/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.open_browser = False" >> /home/$NB_USER/.jupyter/jupyter_notebook_config.py && \
    echo "c.NotebookApp.notebook_dir = '/notebooks'" >> /home/$NB_USER/.jupyter/jupyter_notebook_config.py && \
    chown -R $NB_UID:root /home/$NB_USER && \
    chmod g+rwX,o+rX -R /home/$NB_USER

LABEL io.k8s.description="PySpark Jupyter Notebook." \
      io.k8s.display-name="PySpark Jupyter Notebook." \
      io.openshift.expose-services="8888:http"

ENV TINI_VERSION v0.9.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini.asc /tini.asc
RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys 0527A9B7 && gpg --verify /tini.asc
ADD start.sh /start.sh

RUN export PYTHONPATH=$SPARK_HOME/python:$(echo $SPARK_HOME/python/lib/py4j-*-src.zip)


RUN chmod +x /tini /start.sh

ENV HOME /home/$NB_USER
USER $NB_UID
WORKDIR /notebooks
ADD app.py /notebooks/
ADD test-app2.ipynb /notebooks/
# ADD test-app2.py /notebooks/
# RUN mkdir /datavol1
# ENTRYPOINT ["/tini", "--"]
# CMD ["python","/app.py"]
CMD ["/start.sh"]

# Set the default CMD to print the usage of the language image.
# CMD $STI_SCRIPTS_PATH/usage
