FROM wisesight/ai-based-image
RUN apt-get install -y wget python-dev git
RUN pip3 install cython
RUN wget https://github.com/pytries/datrie/archive/0.7.1.tar.gz 
RUN tar xf 0.7.1.tar.gz 
RUN cd datrie-0.7.1 && ./update_c.sh && python3 setup.py build && python3 setup.py install 
RUN pip3 install https://e3fa3a87c45355b49c30ad03188517d0ca6d797c@github.com/ThothMedia/wiseling/archive/master.zip
