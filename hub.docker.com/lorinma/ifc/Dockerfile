from lorinma/ifc:cpp
MAINTAINER lorinma <malingreal [at] gmail {dot} com
RUN apt-get update -y; apt-get install -y --force-yes --no-install-recommends SWIG
RUN pip install ipdb
RUN cd /usr/local/src/; git clone https://github.com/tpaviot/pythonocc-core.git; cd pythonocc-core; git checkout 0.16.0; mkdir build; cd build; cmake ..; make -j4; make install; cd ../../; rm -rf pythonocc-core
ENV DEV /usr/local/lib/python2.7/dist-packages
ADD http://iweb.dl.sourceforge.net/project/ifcopenshell/0.5.0-preview1/ifcopenshell-python-2.7-0.5.0-preview1-linux64.zip $DEV.zip
RUN unzip $DEV.zip -d $DEV; rm $DEV.zip
