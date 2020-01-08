# ==================================================================
# module list
# ------------------------------------------------------------------
# python        3.6    (apt)
# ==================================================================

FROM ufoym/deepo:all-py36-cpu
RUN APT_INSTALL="apt-get install -y --no-install-recommends" && \
    PIP_INSTALL="python -m pip --no-cache-dir install --upgrade" && \
    GIT_CLONE="git clone --depth 10" && \

    rm -rf /var/lib/apt/lists/* \
           /etc/apt/sources.list.d/cuda.list \
           /etc/apt/sources.list.d/nvidia-ml.list && \

    apt-get update

# ==================================================================
# tools
# ------------------------------------------------------------------
RUN APT_INSTALL="apt-get install -y --no-install-recommends" && \
    PIP_INSTALL="python -m pip --no-cache-dir install --upgrade" && \
    DEBIAN_FRONTEND=noninteractive $APT_INSTALL \
        xfonts-base \
        xfonts-75dpi \
        fonts-nanum fonts-nanum-coding fonts-nanum-extra \
        p7zip-full \
        && \
    wget --quiet https://downloads.wkhtmltopdf.org/0.12/0.12.5/wkhtmltox_0.12.5-1.xenial_amd64.deb -O ~/wkhtml.deb && \
    dpkg -i ~/wkhtml.deb && \
    rm ~/wkhtml.deb
        
# ==================================================================
# python
# ------------------------------------------------------------------
RUN APT_INSTALL="apt-get install -y --no-install-recommends" && \
    PIP_INSTALL="python -m pip --no-cache-dir install --upgrade" && \
 $PIP_INSTALL \
        pdfkit \
        jupyter \
        jupyterlab \
        jupyterthemes \
        jupyter_contrib_nbextensions
        
# ==================================================================
# config & cleanup
# ------------------------------------------------------------------

RUN ldconfig && \
    apt-get clean && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/* /tmp/* ~/*


#COPY run_jupyterlab.sh /root
COPY ./jupyter_config/jupyter_notebook_config.py /root/.jupyter/
#COPY ./jupyter_config/custom/custom.css /root/.jupyter/custom/
COPY ./jupyter_config/custom /root/.jupyter/
COPY synced /root/synced
WORKDIR /root
#RUN chmod +x /run_jupyter.sh
#RUN chmod +x /run_jupyterlab.sh
#CMD ["/run_jupyter.sh", "--allow-root"]

EXPOSE 8888 6006
