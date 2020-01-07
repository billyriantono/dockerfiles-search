FROM jupyter/datascience-notebook

RUN conda config --append channels plotly

RUN conda install -c plotly --quiet --yes \
    'plotly' \
	'plotly_express' \
	'chart-studio' \
	'plotly-geo' \
	&& \
    conda clean --all -f -y
	
RUN conda install -c conda-forge --quiet --yes \
	'black' \
	'jupyterlab_code_formatter' \
	'psycopg2' \
	'pandas-gbq' \
	&& \
	conda clean --all -f -y
	
RUN pip install boto3 mutagen

RUN jupyter labextension install @jupyterlab/plotly-extension

RUN jupyter labextension install @jupyterlab/toc

RUN jupyter labextension install @jupyterlab/celltags

RUN jupyter labextension install @ryantam626/jupyterlab_code_formatter

RUN jupyter serverextension enable --py jupyterlab_code_formatter

RUN jupyter lab clean && jupyter lab build

RUN jupyter lab build