FROM jupyter/base-notebook:notebook-6.0.0
LABEL maintainer "mi2428 <tmiya@protonmail.ch>"

ARG theme="oceans16"

ENV TZ=Asia/Tokyo

COPY assets/custom.css /tmp
COPY assets/scratchpad.patch /tmp
COPY assets/jupyter_notebook_config.py .jupyter

USER root
WORKDIR /

RUN apt-get update \
 && apt-get install -yq --no-install-recommends \
      vim git patch \
 && rm -rf /var/lib/apt/lists/*

USER $NB_UID
WORKDIR $HOME


RUN pip install --upgrade \
      jupyterthemes jupyter_contrib_nbextensions yapf ipyparallel \
      jupyterlab ipykernel bash_kernel \
 && python -m bash_kernel.install \
 && jupyter contrib nbextension install --user \
 && mkdir -p $(jupyter --data-dir)/nbextensions

RUN jt -t ${theme} -vim -T -N -f ubuntu -tf ubuntu -nf ptsans \
      -fs 12 -nfs 12 -tfs 12 -dfs 11 -ofs 11 -lineh 100 --cellw 90% \
 && mv .jupyter/custom/custom.css /tmp/jt.css \
 && cat /tmp/custom.css /tmp/jt.css > .jupyter/custom/custom.css

RUN cd $(jupyter --data-dir)/nbextensions \
 && git clone --depth 1 https://github.com/lambdalisue/jupyter-vim-binding.git \
 && jupyter nbextension install --user jupyter-vim-binding \
 && jupyter nbextension enable --user jupyter-vim-binding/vim_binding \
 && cd -

RUN jupyter serverextension enable --py jupyterlab \
 && jupyter nbextension install --user --py ipyparallel \
 && jupyter nbextension enable --user --py ipyparallel \
 && jupyter serverextension enable --user --py ipyparallel \
 && jupyter nbextension enable --user codefolding/main \
 && jupyter nbextension enable --user scratchpad/main \
 && jupyter nbextension enable --user nbextensions_configurator/config_menu/main \
 && jupyter nbextension enable --user select_keymap/main \
 && jupyter nbextension enable --user splitcell/splitcell \
 && jupyter nbextension enable --user collapsible_headings/main \
 && jupyter nbextension enable --user freeze/main \
 && jupyter nbextension enable --user hide_input/main \
 && jupyter nbextension enable --user hide_input_all/main \
 && jupyter nbextension enable --user move_selected_cells/main \
 && jupyter nbextension enable --user code_prettify/code_prettify \
 && jupyter nbextension enable --user limit_output/main \
 && jupyter nbextension enable --user execute_time/ExecuteTime \
 && jupyter nbextension enable --user printview/main \
 && jupyter nbextension enable --user highlighter/highlighter \
 && jupyter nbextension enable --user python-markdown/main \
 && jupyter nbextension enable --user keyboard_shortcut_editor/main

RUN patch -u $(jupyter --data-dir)/nbextensions/scratchpad/main.js < /tmp/scratchpad.patch

CMD ["jupyter", "lab"]
