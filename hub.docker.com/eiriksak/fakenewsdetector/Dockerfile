# Use an official Python runtime as a parent image
FROM python:3.7-slim

RUN apt update
RUN apt install -y python3-dev gcc

# Install pytorch and fastai
RUN pip --no-cache-dir install torch_nightly -f https://download.pytorch.org/whl/nightly/cpu/torch_nightly.html

#RUN pip install numpy torchvision_nightly
#RUN pip install torch_nightly -f https://download.pytorch.org/whl/nightly/cpu/torch_nightly.html
RUN pip --no-cache-dir install fastai

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Run app.py when the container launches
CMD ["python", "app.py"]