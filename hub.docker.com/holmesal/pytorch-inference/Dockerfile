# Start with the official python image
FROM python:3.7

# Set up the working directory
ENV APP_HOME /app
WORKDIR $APP_HOME

# Update deps
RUN apt-get update

# Instally pytorch *cpu-only* builds
RUN pip3 install torch==1.2.0+cpu torchvision==0.4.0+cpu -f https://download.pytorch.org/whl/torch_stable.html