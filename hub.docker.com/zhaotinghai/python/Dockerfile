FROM zhaotinghai/python:3.6-base

# MAINTAINER zhaotinghai <zhaotinghai@sina.cn>

# RUN pip --no-cache-dir install jupyter notebook jupyter_contrib_nbextensions pymongo apscheduler pystan fbprophet tensorflow==1.13.1 \

RUN pip install --no-cache-dir --upgrade pip && \
pip --no-cache-dir install pandas-datareader keras scipy==1.2.1 statsmodels sklearn seaborn pyecharts jupyterthemes tqdm numba && \
jupyter notebook --generate-config && \
sed -i "s/#c.NotebookApp.ip = 'localhost'/c.NotebookApp.ip = '*'/g" /root/.jupyter/jupyter_notebook_config.py && \
sed -i "s/#c.NotebookApp.allow_remote_access = False/c.NotebookApp.allow_remote_access = True/g" /root/.jupyter/jupyter_notebook_config.py && \
sed -i "s/#c.NotebookApp.allow_root = False/c.NotebookApp.allow_root = True/g" /root/.jupyter/jupyter_notebook_config.py && \
sed -i "s/#c.NotebookApp.open_browser = True/c.NotebookApp.open_browser = False/g" /root/.jupyter/jupyter_notebook_config.py && \
sed -i "s/#c.NotebookApp.port = 8888/c.NotebookApp.port = 8888/g" /root/.jupyter/jupyter_notebook_config.py && \
jupyter contrib nbextension install --user && \
python --version && \
pip list && \
cat /root/.jupyter/jupyter_notebook_config.py | grep c.NotebookApp.

# CMD jupyter notebook --ip="*" --allow-root --no-browser --port=8888 --notebook-dir=/data/notebook/
