FROM jjanzic/docker-python3-opencv:contrib-opencv-3.4.1

RUN \
  mkdir /src && \
  mkdir /data && \
  apt-get update && \
  apt-get upgrade -y && \
  apt-get install -y curl git && \
  pip install --upgrade pip && \
  pip install cython tensorflow

RUN \
  mkdir /src/darkflow && \
  git clone https://github.com/thtrieu/darkflow.git /src/darkflow && \
  cd /src/darkflow && \
  python setup.py build_ext --inplace && \
  mkdir bin && \
  curl -o bin/yolov2.weights https://pjreddie.com/media/files/yolov2.weights

RUN \
  pip install jupyter

WORKDIR src

# add your data & source code directly below, or mount them
# in a volume 

#ADD ../data/* /data/
#ADD ../src/* /src/

# run model on test footage if you would like to test the installation

# CMD \
#   python flow --model cfg/yolo.cfg --load bin/yolov2.weights \
#   --demo /data/testFootage.mp4 --saveVideo && \
#   mv video.avi /out/.

CMD jupyter notebook --no-browser --ip 0.0.0.0 --allow-root
