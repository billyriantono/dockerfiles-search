FROM continuumio/anaconda

WORKDIR  /app
RUN mkdir /app/notebooks
EXPOSE 8888
CMD ["jupyter", "notebook", "--allow-root", "--notebook-dir=/app/notebooks", "--ip='*'", "--port=8888", "--no-browser"]
