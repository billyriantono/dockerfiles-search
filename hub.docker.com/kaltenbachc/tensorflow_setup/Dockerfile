# gets latest tensorflow with python3 and jupyter notebook

FROM tensorflow/tensorflow:latest-gpu-py3-jupyter

COPY install_rabbitmq.sh /installation/
COPY tensorflow_test.py /installation/

# Installing RabbitMQ now
RUN bash /installation/install_rabbitmq.sh

# Installing python packages
RUN pip install pika
RUN pip install matplotlib 
RUN pip install tables
RUN pip install theano
RUN pip install pandas
RUN pip install scikit-image
RUN pip install peakutils

# Check if tensorflow and GPU work properly 
CMD python /installation/tensorflow_test.py