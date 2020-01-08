FROM python:3.7

RUN git clone git://github.com/manusetty/wishbone.git

RUN pip install Cython && cd wishbone && pip3 install .

COPY ./traj-converters /home/traj-converters

#opens a bash shell with -it
CMD ["/bin/bash"]

