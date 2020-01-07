FROM continuumio/miniconda3

SHELL ["/bin/bash", "-c"]

RUN apt update && apt install -y gcc g++ 
RUN conda config --append channels conda-forge && conda update conda -y --quiet 

RUN conda create --name py35 python=3.5 cython numpy scipy nose matplotlib pytest coverage flake8 sphinx nbsphinx sphinx_rtd_theme numpydoc jupyter ipython "pandoc>=1.12.1,<2.0.0" -y --quiet
ENV PATH /opt/conda/envs/py35/bin:$PATH
RUN /bin/bash -c "source activate py35"
RUN pip install --upgrade --quiet pip && pip install qutip flake8-colors flake8-docstrings flake8-import-order sphinx_autodoc_typehints

RUN conda create --name py36 python=3.6 cython numpy scipy nose matplotlib pytest coverage flake8 sphinx nbsphinx sphinx_rtd_theme numpydoc jupyter ipython "pandoc>=1.12.1,<2.0.0" -y --quiet
ENV PATH /opt/conda/envs/py36/bin:$PATH
RUN /bin/bash -c "source activate py36"
RUN pip install --upgrade --quiet pip && pip install qutip flake8-colors flake8-docstrings flake8-import-order sphinx_autodoc_typehints

RUN conda create --name py37 python=3.7 cython numpy scipy nose matplotlib pytest coverage flake8 sphinx nbsphinx sphinx_rtd_theme numpydoc jupyter ipython "pandoc>=1.12.1,<2.0.0" -y --quiet
ENV PATH /opt/conda/envs/py37/bin:$PATH
RUN /bin/bash -c "source activate py37"
RUN pip install --upgrade --quiet pip && pip install qutip flake8-colors flake8-docstrings flake8-import-order sphinx_autodoc_typehints
