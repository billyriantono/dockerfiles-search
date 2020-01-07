FROM jjanzic/docker-python3-opencv:opencv-3.4.1

ENV DLIB_TAG="v19.16"


RUN apt-get update && \
	apt-get install -y libatlas-base-dev

RUN cd /root && \
    git clone -b $DLIB_TAG --single-branch https://github.com/davisking/dlib.git && \
    cd  dlib/ && \
    python3 setup.py install --yes USE_AVX_INSTRUCTIONS

WORKDIR /root/dlib/python_examples
RUN wget -q http://dlib.net/files/shape_predictor_5_face_landmarks.dat.bz2 && \
	wget -q http://dlib.net/files/dlib_face_recognition_resnet_model_v1.dat.bz2 && \
	bzip2 -d *bz2
