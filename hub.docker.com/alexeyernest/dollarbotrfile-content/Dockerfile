FROM python:3.6
RUN apt update && apt install libavdevice-dev libavfilter-dev libopus-dev libvpx-dev pkg-config python-psycopg2 python-opencv python-pip cmake git -y && apt clean
RUN pip3 install dlib imutils scipy numpy cognitive_face tensorflow av uwsgi psycopg2
