FROM usgsastro/miniflask
RUN conda install -c conda-forge flask redis
RUN pip install redis
ADD . /app
WORKDIR /app

EXPOSE 5000
CMD ["python", "redisjson.py"]
