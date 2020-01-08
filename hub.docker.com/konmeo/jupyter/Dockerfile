FROM konmeo/flask-dev

MAINTAINER konmeo

EXPOSE 8888

WORKDIR /workspace

RUN pip3 install --no-cache-dir \
        jupyter jupyter-contrib-nbextensions jupyterthemes \
        ipywidgets ipyparallel yapf hide_code nbdime qgrid

RUN sed -i "s/\(matplotlib.use\)/pass # \1/g" \
        /usr/local/lib/python3.6/site-packages/backtrader/plot/*.py

COPY jupyter-notebook.py /usr/local/bin/

USER user

RUN ipython profile create && \
    ipcluster nbextension enable --user && \
    jupyter contrib nbextension install --user && \
    jupyter nbextensions_configurator enable --user && \
    \
    jupyter nbextension enable --user --py widgetsnbextension && \
    jupyter nbextension enable --user chrome-clipboard/main && \
    jupyter nbextension enable --user codefolding/main && \
    jupyter nbextension enable --user code_font_size/code_font_size && \
    jupyter nbextension enable --user code_prettify/code_prettify && \
    jupyter nbextension enable --user comment-uncomment/main && \
    jupyter nbextension enable --user execute_time/ExecuteTime && \
    jupyter nbextension enable --user freeze/main && \
    jupyter nbextension enable --user hide_input/main && \
    jupyter nbextension enable --user hide_input_all/main && \
    jupyter nbextension enable --user scratchpad/main && \
    jupyter nbextension enable --user scroll_down/main && \
    jupyter nbextension enable --user select_keymap/main && \
    jupyter nbextension enable --user skip-traceback/main && \
    jupyter nbextension enable --user splitcell/splitcell && \
    jupyter nbextension enable --user table_beautifier/main && \
    jupyter nbextension enable --user toc2/main && \
    jupyter nbextension enable --user toggle_all_line_numbers/main && \
    \
    jupyter nbextension install --user --py hide_code && \
    jupyter nbextension enable --user --py hide_code && \
    jupyter nbextension enable --user --py qgrid && \
    jupyter serverextension enable --user --py hide_code && \
    \
    nbdime reg-extensions --user

RUN jt -t monokai -f firacode -altp -vim -fs 10 -nfs 10 -tfs 10 -cellw 90%

CMD ["/usr/local/bin/jupyter-notebook.py"]
