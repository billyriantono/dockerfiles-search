FROM jupyterhub/singleuser:latest
LABEL MAINTAINER Quang Dang <quanghd96@gmail.com>

# install numpy: 
RUN pip install numpy
# install pandas: 
RUN pip install pandas
# install matplotlib: 
RUN pip install matplotlib
# install sklearn: 
RUN pip install sklearn

RUN jupyter notebook --generate-config -y
RUN echo "c.NotebookApp.token=''">>~/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.password=u''">>~/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.ip = '*'">>~/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.open_browser = False">>~/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.allow_origin = '*'">>~/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.disable_check_xsrf = True">>~/.jupyter/jupyter_notebook_config.py
RUN echo "c.GatewayClient.validate_cert = True">>~/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.tornado_settings = {\
    'headers': {\
    'Content-Security-Policy': 'frame-ancestors self http://localhost:4200 https://*.tri-arrow.co.jp',\
    }\
    }" >>~/.jupyter/jupyter_notebook_config.py

COPY custom.js /home/jovyan/.jupyter/custom/
