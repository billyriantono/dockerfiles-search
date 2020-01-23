FROM microsoft/vsts-agent:ubuntu-16.04

# Install Miniconda
RUN curl -sL https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -o miniconda.sh \
 && chmod +x miniconda.sh \
 && ./miniconda.sh -b -p /usr/share/miniconda \
 && rm miniconda.sh
ENV CONDA=/usr/share/miniconda
ARG CONDA=/usr/share/miniconda

# install conda libraries to base conda
RUN /bin/bash -c "source $CONDA/bin/activate \
  && conda config --add channels conda-forge \
  && conda install -y pyproj>=2.2 shapely cartopy descartes lxml numpy scipy matplotlib pandas \
  && rm -rf $CONDA/pkgs/*"
# install key python libraries
RUN /bin/bash -c "source $CONDA/bin/activate \ 
  && pip install geopandas contextily pint folium IPython beautifulsoup4 requests astropy NavPy geopy"
# install key docs packages
RUN /bin/bash -c "source $CONDA/bin/activate \
  && pip install pbr docutils sphinx"
RUN /bin/bash -c "source $CONDA/bin/activate \
  && pip install sphinx-autodoc-napoleon-typehints javasphinx sphinx-fortran \
sphinx-git sphinx-markdown-builder \
sphinxcontrib-autojs sphinxcontrib-packages sphinxcontrib-needs sphinxcontrib-jupyter sphinx-autodoc-annotation \
sphinxcontrib-issuetracker sphinxcontrib-domaintools sphinxcontrib-adadomain \
sphinxcontrib-makedomain sphinxcontrib-matlabdomain sphinx-paramlinks sphinxcontrib-plantuml \
sphinxcontrib-requirements sphinxcontrib-email stdeb sphinxpapyrus-docxbuilder"
# install key python testing libraries
RUN /bin/bash -c "source $CONDA/bin/activate \
  && pip install mypy autopep8 pydocstyle \
pytest pytest-cov pytest-asyncio pytest-pylint \
mypy radon>=2.4.0 flake8 pylint asynctest \
nose autopep8 gitpython nbconvert jupyter_client pbr" 
# install key documentation libraries
#RUN apt-get update && \
#  apt-get install -y librsvg2-bin latexmk tex-common tex-gyre fonts-freefont-otf texlive-xetex texlive-fonts-recommended graphviz dvipng librsvg2-bin && \
#  rm -rf /var/lib/apt/lists/*

# Install other key utilities
RUN apt-get update && \
  apt-get install -y make && \
  rm -rf /var/lib/apt/lists/*


# Clean system
RUN apt-get clean \
 && rm -rf /var/lib/apt/lists/* \
 && rm -rf /etc/apt/sources.list.d/*

RUN chown -R 1001:1001 $CONDA

ENV PATH $CONDA/condabin/:$CONDA/bin/:$PATH
CMD /bin/bash && source $CONDA/bin/activate
