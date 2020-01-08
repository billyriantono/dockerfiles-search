FROM jupyter/datascience-notebook

RUN pip install git+git://github.com/derekpowell/dmppy.git \
  && conda install -c conda-forge jupyter_contrib_nbextensions -y --quiet \
  && jupyter nbextension enable codefolding/main \
  && jupyter nbextension enable limit_output/main \
  && jupyter nbextension enable scratchpad/main \
  && jupyter nbextension enable code_prettify/main \
  && jupyter nbextension enable tree-filter/main
