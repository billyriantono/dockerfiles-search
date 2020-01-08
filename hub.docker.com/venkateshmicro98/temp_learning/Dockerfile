FROM python:3

#environment variable
ENV QT_X11_NO_MITSHM=1

#working directory inside the container
WORKDIR /usr/src/opencv_tutorial

#requirements file will have all the python dependent packages
COPY requirements.txt ./

RUN apt-get update && apt-get install -y \
    python3-opencv \
    python3-pip

#this will download the packages mentioned in requirements.txt
RUN pip3 install -r requirements.txt

#copy everything from local to image
COPY . .

#CMD [ "python3", "myapp.py" ]
#CMD tail -f /dev/null
