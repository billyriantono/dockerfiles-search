FROM julia:1.1.1
MAINTAINER SATOSHI TERASAKI
# for Jupyter
EXPOSE 8888 
# suppress message like below:
# debconf: delaying package configuration, since apt-utils is not installed
# suppress GTK warnings about accessibility because there's no dbus
# ** (julia:365): WARNING **: Couldn't connect to accessibility bus: Failed to connect to socket /tmp/dbus-HNlhMfzYuj: Connection refused
ENV NO_AT_BRIDGE 1
ENV DEBCONF_NOWARNINGS yes
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    bzip2 \
    gettext \
    fbi \
    imagemagick \
    libcanberra-gtk-module \
    libcanberra-gtk3-module \
    libgtk-3-dev \
    libffi-dev \
    python3-tk \
    qt5-default \
    wget

# install python env and connect with PyCall.jl
RUN julia -e 'ENV["PYTHON"]="";\
              using Pkg; Pkg.add(["PyCall", "Conda"]); \
              using Conda; Conda.add("python=3.6.*"); \
              Pkg.build("PyCall"); using PyCall'
# enable to call python and jupyter from bash
ENV PATH="/root/.julia/conda/3/bin:$PATH:${PATH}"
# install python libraries via Conda.jl
RUN julia -e 'using Pkg, Conda;\
              Conda.add(["matplotlib","sympy","jupyter"]);\
              Pkg.add(["PyPlot","SymPy","IJulia"]);\
              using PyPlot, SymPy, IJulia'
# for Juno(IDE; extension of Atom Editor)
RUN julia -e 'using Pkg; Pkg.add(["Atom", "Juno"])'
# add developer utility
RUN julia -e 'using Pkg;\
              Pkg.add(["BenchmarkTools", "Debugger", "JuliaInterpreter", "PackageCompiler", "Revise"]);\
              using BenchmarkTools, Debugger, Distributed, JuliaInterpreter, PackageCompiler, Revise'
# add Julia Packages
RUN julia -e 'using Pkg;\
              Pkg.add(["UnicodePlots", "GR", "Plots"]);\
              using UnicodePlots, GR, Plots'
# add Image packages 
# build dependency
RUN cd /tmp && \
    wget http://zlib.net/zlib-1.2.11.tar.gz && \
    tar xvzf zlib-1.2.11.tar.gz && \
    cd zlib-1.2.11 && ./configure && make && make install && \
    cd .. && rm -r zlib-1.2.11
RUN julia -e 'using Pkg;\
              Pkg.add(["Images", "ImageMagick", "ImageMetadata", "TestImages"]);\
              using Images, ImageMagick, ImageMetadata, TestImages'
# Do not import[using] Cairo, Gtk and ImageView here.
# It will cause initialization error because of its image does not have X server
# https://github.com/JuliaGraphics/Gtk.jl/issues/378
# https://github.com/JuliaImages/ImageView.jl/issues/158
RUN julia -e 'using Pkg;\
              Pkg.add(["Cairo", "Gtk"]);\
              Pkg.add("ImageView")'
# add utility
RUN julia -e 'using Pkg;\
              Pkg.add(["ArgParse", "Distributed"]);\
              using ArgParse, Distributed'

# compile Plots to reduce overhead of `using Plots`
# this layer fails on MacOS and Windows Host
#RUN julia -e 'using Pkg;\
#              using PackageCompiler; compile_package("Plots",force=true);\
#              using Plots'
RUN apt-get update && apt-get install -y fbi
#clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/*
