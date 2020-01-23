FROM goofts/hummingbirds:latest

MAINTAINER goofts loking.zhao.moshang@icloud.com

ENV HUMMINGBIRDS_VERSION 3.5.8

ENV PYTHON_PACKAGES /usr/local/lib/python3*/dist-packages

ENV LAB_PATH=/usr/share/jupyter/lab

ENV LATEX_PATH=/hummingbirds/extension/latex

ENV LTITLE "s;<title>JupyterLab</title>;<title>Python - Hummingbirds</title>;g"

ENV NTITLE "s;<title>Python - Hummingbirds</title>;<title>Clang - Hummingbirds</title>;g"

ENV CMAP_URL="s;i.cMapUrl;location.href.split('lab')[0]+'static/lab/cmaps/';g"

ENV CMAP_ENABLE="s;i.cMapPacked;true;g"

USER root

WORKDIR /root

run apt update && apt install -y texlive-xetex latex-cjk-all                      && \
    jupyter labextension install @jupyterlab/latex && apt purge -y cpp* ruby* tk* && \
    npm cache clean -f && apt autoremove -y && apt autoclean && apt clean         && \
    find /usr/lib/python* -name __pycache__ | xargs rm -rf                        && \
    find /usr/local/lib/python* -name __pycache__ | xargs rm -rf                  && \
    rm -rf ~/* ~/.[^jvp\.]* /tmp/* /var/tmp/* /var/cache/apt/*                    && \
    rm -rf /usr/local/share/.[0-9a-zA-Z]* /usr/local/share/*                      && \
    rm -rf /usr/share/jupyter/lab/staging/build/* /usr/share/jupyter/kernels/*

run sed -i "$CMAP_URL"    $LAB_PATH/static/vendors~pdfjs.*.js                         && \
    sed -i "$CMAP_ENABLE" $LAB_PATH/static/vendors~pdfjs.*.js                         && \
    sed -i "$NTITLE"      $PYTHON_PACKAGES/notebook/templates/page.html               && \
    sed -i "$LTITLE"      $LAB_PATH/static/index.html                                 && \
    cp -rf $LAB_PATH/staging/node_modules/pdfjs-dist/cmaps $LAB_PATH/static           && \
    cp -rf $LATEX_PATH/vimrc ~/.vimrc && cp -rf $LATEX_PATH/vimrc /home/goofts/.vimrc && \
    cp -rf $LATEX_PATH/pdf.js $LAB_PATH/staging/node_modules/pdfjs-dist/build/        && \
    npm cache clean -f && apt autoremove && apt autoclean && apt clean                && \
    find /usr/lib/python* -name __pycache__ | xargs rm -rf                            && \
    find /usr/local/lib/python* -name __pycache__ | xargs rm -rf                      && \
    rm -rf ~/* ~/.[^jvp\.]* /tmp/* /var/tmp/* /var/cache/apt/*                        && \
    rm -rf /usr/local/share/.[0-9a-zA-Z]* /usr/local/share/*                          && \
    rm -rf /usr/share/jupyter/lab/staging/build/* /usr/share/jupyter/kernels/*
