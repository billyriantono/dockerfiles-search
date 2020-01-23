FROM aibakevision/object-detector-base-gpu:cuda8.0-ubuntu16.04-python3.5.2

# Make workspace
RUN mkdir /workspace/webapp
ADD entrypoint.sh /workspace/webapp
ADD ./src /workspace/webapp
WORKDIR /workspace/webapp

# Set aws config file path
ARG aws_config_file=/workspace/webapp/.aws/config
ENV AWS_CONFIG_FILE=${aws_config_file}
RUN echo $AWS_CONFIG_FILE

# Download pre-trained weights
ARG s3_dataset_path=s3://aibakevision-object-detection/darknet/weights
RUN aws s3 sync ${s3_dataset_path} /workspace/webapp

# Install dependencies of python application
RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt

#EXPOSE 5002
ENTRYPOINT ["/bin/bash", "entrypoint.sh"]


