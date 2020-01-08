FROM continuumio/miniconda3

RUN apt-get update -qq && \
    apt-get install -qq fonts-ipaexfont-gothic && \
    apt-get clean -qq && \
    conda update -q -y -n base conda && \
    conda install -q -y jupyter numpy scipy scikit-learn scikit-image pandas matplotlib && \
    conda install -q -y -c conda-forge jupyter_contrib_nbextensions rise && \
    conda clean -a -y && \
    jupyter nbextension install rise --py && \
    jupyter nbextension enable rise --py && \
    jupyter nbextension enable execute_time/ExecuteTime && \
    jupyter nbextension enable freeze/main && \
    jupyter nbextension enable hinterland/hinterland && \
    jupyter nbextension enable scratchpad/main && \
    mkdir -p $HOME/.config/matplotlib && \
    echo "font.family : IPAexGothic" > $HOME/.config/matplotlib/matplotlibrc

VOLUME ["/data"]
WORKDIR /data

EXPOSE 8888

ENTRYPOINT ["tini", "--"]
CMD ["jupyter", "notebook", "--no-browser", "--allow-root", "--ip='*'", "--NotebookApp.token=''"]
