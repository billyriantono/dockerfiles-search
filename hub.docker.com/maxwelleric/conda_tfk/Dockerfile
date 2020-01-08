FROM continuumio/anaconda3:5.2.0

WORKDIR  /app
RUN mkdir /app/notebooks

RUN conda config --set ssl_verify False
RUN conda install -c anaconda tensorflow
RUN conda install -c anaconda keras

EXPOSE 8888

CMD ["jupyter", "notebook", "--allow-root", "--notebook-dir=/app/notebooks", "--ip='*'", "--port=8888", "--no-browser"]
