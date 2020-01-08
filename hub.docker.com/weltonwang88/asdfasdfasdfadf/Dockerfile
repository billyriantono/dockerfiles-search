FROM python:3.7
RUN pip install numpy torch fastai Flask pytorch-pretrained-bert 
WORKDIR /src
RUN pip install rncryptor gdown
RUN gdown https://drive.google.com/uc?id=1LEtEHzH17epbJWEnSdybIO8Xj5s3t0q-

# Copy our code from the current folder to /app inside the container
COPY . /src/
# Make port 8080 available for links and/or publish
EXPOSE 8080

# Define our command to be run when launching the container

CMD ["python", "app.py"]
