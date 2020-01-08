FROM ubuntu:latest
RUN apt-get update -qq && apt-get install -y build-essential git python3 python3-dev python3-pip
RUN pip3 install --upgrade pip
RUN pip3 install wandb pandas scikit-learn tensorflow keras h5py flask scikit-image scipy pillow
RUN mkdir /work
WORKDIR /work
