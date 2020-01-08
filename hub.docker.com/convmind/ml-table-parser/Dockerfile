# Use Caffe2 image as parent image
FROM caffe2/caffe2:snapshot-py2-cuda9.0-cudnn7-ubuntu16.04

RUN mv /usr/local/caffe2 /usr/local/caffe2_build
ENV Caffe2_DIR /usr/local/caffe2_build

ENV PYTHONPATH /usr/local/caffe2_build:${PYTHONPATH}
ENV LD_LIBRARY_PATH /usr/local/caffe2_build/lib:${LD_LIBRARY_PATH}
WORKDIR /app

# Clone the Detectron repository
COPY ./requirements.txt /app


# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

COPY . . 

# Install the COCO API
RUN git clone https://github.com/cocodataset/cocoapi.git /cocoapi
WORKDIR /cocoapi/PythonAPI
RUN make install

# Go to Detectron root
WORKDIR /app

# Set up Python modules
RUN make
RUN mkdir /app/configs && cd /app/configs && curl -O "https://convmind-models.s3.us-east-2.amazonaws.com/basic-models/config_X152.yaml" && \
    curl -O "https://convmind-models.s3.us-east-2.amazonaws.com/basic-models/model_final.pkl"

# [Optional] Build custom ops
#EXPOSE 9976
#CMD [ "gunicorn", "-b", "0.0.0.0:9976", "-w", "4", "-t", "300", "wsgi:application"]
CMD [ "python", "convert_table.py"]
