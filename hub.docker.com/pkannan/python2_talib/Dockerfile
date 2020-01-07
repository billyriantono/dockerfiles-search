#-----------------------------------------------------------------------------------------------------
# References:
# 1. ta-lib installation: https://github.com/quantopian/zipline/blob/master/Dockerfile
# 2. tini Installation: https://hub.docker.com/r/continuumio/anaconda/~/dockerfile/
# 3. Anaconda Installation: https://hub.docker.com/r/continuumio/anaconda/~/dockerfile/
# 4. https://www.continuum.io/blog/developer-blog/anaconda-and-docker-better-together-reproducible-data-science
# 5. http://www.projectatomic.io/docs/docker-image-author-guidance/
#
# Installed Software : 
#   1. tini
#       Add Tini. Tini operates as a process subreaper for jupyter. This prevents kernel crashes.                                                                              
#
#   2. ta-lib (http://ta-lib.org)
#       Multi-Platform Tools for Market Analysis
#
#   3. Miniconda
#       conda package manager and Python from continuumio
# 
#   4. OS LeveL Dependancies Installs and Which (TODO: Need to update)?
#       a. matplotlib  |  libav-tools 
#       b. ta-lib      |       
#-----------------------------------------------------------------------------------------------------
FROM ubuntu:16.04
MAINTAINER "Priyesh Kannan" 
RUN     apt-get update --fix-missing \
    &&  apt-get install -y --no-install-recommends curl grep sed dpkg bzip2 make ca-certificates \
    &&  apt-get install -y --no-install-recommends libglib2.0-0 libxext6 libsm6 libxrender1 libav-tools\
    &&  apt-get install -y --no-install-recommends libfreetype6-dev libpng-dev libopenblas-dev liblapack-dev gfortran \
    &&  apt-get install -y --no-install-recommends texlive texlive-latex-extra pandoc \
    &&  apt-get clean

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8 \
    ANACONDA_URL="https://repo.continuum.io/archive/Anaconda2-4.2.0-Linux-x86_64.sh" \
    TALIB_URL="https://downloads.sourceforge.net/project/ta-lib/ta-lib/0.4.0/ta-lib-0.4.0-src.tar.gz" 

RUN     curl -s -L "${TALIB_URL}" | tar xvz \
    &&  cd ta-lib \
    &&  ./configure --prefix=/usr \
    &&  make \
    &&  make install

RUN TINI_VERSION=`curl https://github.com/krallin/tini/releases/latest | grep -o "/v.*\"" | sed 's:^..\(.*\).$:\1:'` \
    && curl -s -L "https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini_${TINI_VERSION}.deb" -o tini.deb \
    && dpkg -i tini.deb \
    && chmod +x /usr/bin/tini \
    && rm tini.deb 
                                                                                                                                                                                                                    
ARG user=developer

ENV PATH=/home/$user/conda/bin:$PATH

RUN useradd -ms /bin/bash $user -p $(openssl passwd -1 $user) -s /sbin/nologin \
    && mkdir /home/$user/profile.d \
    && chown -R $user:$user  /home/$user \ 
    && ANACONDA_URL="https://repo.continuum.io/archive/Anaconda2-4.2.0-Linux-x86_64.sh" \ 
    && curl -L "${ANACONDA_URL}" -o /tmp/anaconda.sh \
    && chown $user:$user /tmp/anaconda.sh

USER $user

RUN /bin/bash /tmp/anaconda.sh -b -p /home/$user/conda \
    && rm /tmp/anaconda.sh  \
    && conda update --quiet --yes anaconda \
    && conda update --quiet --yes --all \
    && conda update --quiet --yes numpy matplotlib statsmodels scikit-learn jupyter\
    && conda install --quiet --yes seaborn \
    && conda install --quiet --yes -c quantopian ta-lib \
    && pip install pdfminer

RUN mkdir /home/$user/.jupyter \
    && echo "c.NotebookApp.open_browser=False" >  /home/$user/.jupyter/jupyter_notebook_config.py \
    && echo "c.NotebookApp.ip='0.0.0.0'"  >>  /home/$user/.jupyter/jupyter_notebook_config.py \
    && echo "c.NotebookApp.port=8888"  >>  /home/$user/.jupyter/jupyter_notebook_config.py \
    && echo "c.NotebookApp.password=u'"$(python -c "from IPython.lib import passwd ; password = passwd('$user') ; print password")"'" >>  /home/$user/.jupyter/jupyter_notebook_config.py

VOLUME ["/home/$user/apps"]
WORKDIR "/home/$user/apps"
EXPOSE 8888
ENTRYPOINT ["/usr/bin/tini", "--"]
CMD ["jupyter","notebook","--debug"]
