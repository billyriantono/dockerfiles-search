FROM jpambrun/ml-base
RUN mkdir /notebooks && chmod a+rwx /notebooks
RUN mkdir /.local && chmod a+rwx /.local
WORKDIR /notebooks
EXPOSE 8888

RUN pip install jupyterlab itkwidgets
RUN jupyter labextension install @jupyter-widgets/jupyterlab-manager itk-jupyter-widgets

RUN npm install --unsafe-perm -g ijavascript && ijsinstall

CMD ["bash", "-c", "jupyter lab --notebook-dir=/notebooks --ip 0.0.0.0 --no-browser --allow-root  --NotebookApp.token=''"]
