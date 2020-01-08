FROM gettyimages/spark:2.3.0-hadoop-2.8

RUN pip install --upgrade jupyter 
RUN pip install --upgrade findspark

EXPOSE 8888

CMD jupyter notebook --port=8888 --ip=0.0.0.0 --no-browser --allow-root --NotebookApp.token=''
