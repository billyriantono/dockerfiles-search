FROM jupyter/minimal-notebook

USER root

LABEL maintainer="Eric Lau"\
    description="container for shoe scaner data processing"

# run command to install needed packages
RUN apt-get update && apt-get -y install sudo && sudo apt-get upgrade -y && sudo apt-get dist-upgrade -y && \
    sudo apt-get install git libssl-dev libusb-1.0-0-dev pkg-config libgtk-3-dev -y && \
    sudo apt-get install libglfw3-dev libgl1-mesa-dev libglu1-mesa-dev -y && \
    sudo apt-get install cmake -y

# build librealsense
RUN git clone https://github.com/IntelRealSense/librealsense.git /app/librealsense && \
    mkdir /app/librealsense/build && \
    cd /app/librealsense/build && \
    cmake ../ -DBUILD_PYTHON_BINDINGS=bool:true -DBUILD_EXAMPLES=true && \
    sudo make uninstall && \
    make clean && \
    make && \
    sudo make install

# install needed python packages
RUN pip install pyrealsense2 && \
    conda install pandas -y && \
    conda install matplotlib -y && \
    conda install scipy -y && \
    conda install bokeh -y && \
    conda install opencv -y && \
    conda install ipympl -y && \
    conda install -c conda-forge ipywidgets -y && \
    conda install nodejs -y && \
    conda install -c anaconda ipython && \
	conda install xlrd -y && \
    jupyter labextension install @jupyter-widgets/jupyterlab-manager && \
    jupyter labextension install jupyter-matplotlib && \
    jupyter labextension install ipyvolume && \
    jupyter labextension install jupyter-threejs && \
	conda clean -y -all

# set working dir
WORKDIR /app

# expose port
EXPOSE 8888

# make volume for local data to be mounted into
VOLUME /app

# start jupyter lab
CMD ["jupyter", "lab", "--allow-root"]

