FROM ubuntu:18.10
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y curl aptitude python3.6 tesseract-ocr python3-pip libxrender-dev libsm6 libxext6
RUN pip3 install matplotlib pytesseract imutils pytest requests yoyo-migrations psycopg2-binary boto3 Flask environs apscheduler tensorflow keras opencv-contrib-python sklearn


