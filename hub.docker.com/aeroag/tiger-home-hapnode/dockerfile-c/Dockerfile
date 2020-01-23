FROM ubuntu:19.10
RUN apt-get update && apt-get install -y python python-pip git
RUN pip install 'lmdb==0.96' 'numpy==1.16.4'
COPY src /app
WORKDIR /app
VOLUME input_images
CMD [ "python", "./create_data_distribution.py" ]
