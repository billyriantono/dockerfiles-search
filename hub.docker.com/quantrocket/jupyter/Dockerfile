FROM quantrocket/anaconda3-uwsgi
MAINTAINER QuantRocket <support@quantrocket.com>

# Install ta-lib
RUN apt-get -y update && apt-get -y install \
    build-essential \
    libfreetype6-dev \
    libpng-dev \
    libopenblas-dev \
    liblapack-dev \
    gfortran \
    && cd /tmp \
    && curl -L http://prdownloads.sourceforge.net/ta-lib/ta-lib-0.4.0-src.tar.gz | tar xvz \
    && cd ta-lib \
    && ./configure --prefix=/usr \
    && make \
    && make install \
    && pip install TA-Lib==0.4.16 \
    && cd /tmp \
    && rm -r ta-lib

ENV HOUSTON_URL=http://houston ALPHALENS_VERSION=0.3.2 PYFOLIO_VERSION=qr0.9.0.8 \
  SHELL=/bin/bash YOU_ARE_INSIDE_JUPYTER=true MOONSHOT_CACHE_DIR=/codeload/.moonshot_tmp

# (zip is for backups)
RUN apt-get -y update && apt-get -y install zip

RUN /bin/bash -c "source activate /opt/conda" \
  && pip install https://codeload.github.com/quantrocket-llc/pyfolio/zip/${PYFOLIO_VERSION} \
  && pip install https://codeload.github.com/quantopian/alphalens/zip/v${ALPHALENS_VERSION} \
  && pip install -U quantrocket-client \
  && pip install argcomplete \
  && pip install quantrocket-moonchart \
  && pip install quantrocket-moonshot \
  && /bin/bash -c "source deactivate"

RUN conda install -c https://metachannel.conda-forge.org/conda-forge/jupyterlab,notebook,nodejs,numpy,qgrid \
   jupyterlab=1.1.3 \
   notebook=6.0.1 \
   nodejs=10.13.0 \
   # Numpy disappears if I don't specify it here
   numpy=1.14.3 \
   qgrid=1.1.1

RUN npm install -g json2yaml wscat

# QGrid (broken with JupyterLab 1.x - see https://github.com/quantopian/qgrid/issues/261)
RUN jupyter labextension install \
    @jupyter-widgets/jupyterlab-manager@1.0 \
    && git clone https://github.com/qzchenwl/qgrid  /usr/src/qgrid.git  --depth 1 \
    && jupyter labextension install /usr/src/qgrid.git/js/

# IB Gateway GUI extension
COPY jupyterlab_quantrocket /usr/src/jupyterlab_quantrocket
RUN jupyter labextension install /usr/src/jupyterlab_quantrocket/

COPY bashrc /root/.bashrc
# this produces annoying deprecation warnings in current conda version so make
# user do it themselves
# RUN conda init bash
COPY profile_default /root/.ipython/profile_default
COPY sitecustomize /tmp/
RUN bash /tmp/install_sitecustomize.sh
COPY overrides.json /opt/conda/share/jupyter/lab/settings/
COPY templates /etc/opt/quantrocket/templates
COPY bin /opt/quantrocket/bin

EXPOSE 80

CMD ["/bin/bash", "/opt/quantrocket/bin/start.sh"]
