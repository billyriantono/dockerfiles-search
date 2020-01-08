FROM konmeo/jupyter

MAINTAINER konmeo

EXPOSE 8888

WORKDIR /workspace

USER root

RUN pip3 install --no-cache-dir jupyterlab==0.32.1 jupyterlab_github && \
    \
    jupyter labextension install \
        qgrid jupyterlab_discovery jupyterlab_vim \
        @jupyter-widgets/jupyterlab-manager @jupyterlab/github \
        @jupyterlab/plotly-extension jupyterlab_bokeh jupyterlab-drawio && \
    \
    cd /usr/local/share/jupyter/lab/staging && \
    npm prune
    
RUN mkdir /fira && \
    cd /fira && \
    curl -sLO https://github.com/tonsky/FiraCode/releases/download/1.205/FiraCode_1.205.zip && \
    busybox unzip -q *.zip && \
    cd /usr/local/share/jupyter/lab/themes/@jupyterlab && \
    mkdir -p *-dark-*/fonts && \
    cp /fira/ttf/FiraCode-Regular.ttf /fira/ttf/FiraCode-Bold.ttf *-dark-*/fonts/. && \
    rm -rf *-light-*/fonts *-dark-*/fonts/SourceCodePro*.ttf && \
    ln -s ../theme-dark-extension/fonts *-light-*/. && \
    rm -rf /fira && \
    pwd && find -name '*.ttf' && \
    sed -i -e "s/Source Code Pro/Fira Code/g" -e "s/SourceCodePro/FiraCode/g" \
        -e "s/\(code-font-size:\) .*px/\1 15px/g" \
        /usr/local/share/jupyter/lab/themes/@jupyterlab/*/*.css
    
COPY jupyter-notebook.add.py /tmp/
RUN (head -n-2 /usr/local/bin/jupyter-notebook.py; cat /tmp/jupyter-notebook.add.py) \
    > /tmp/jupyter-notebook.py && \
    chmod a+x /tmp/jupyter-notebook.py && \
    mv /tmp/jupyter-notebook.py /usr/local/bin/jupyter-notebook.py && \
    rm /tmp/jupyter-notebook.add.py

USER user

RUN jupyter serverextension enable --user --py jupyterlab_github
