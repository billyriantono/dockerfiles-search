FROM nightseas/cuda-torch

# Update apt-get and install common packages before doing anything else
RUN apt-get -y update

# Installing luarocks and necessary packages
RUN luarocks install tds
RUN luarocks install class
RUN luarocks install nn
RUN luarocks install nngraph

# Install Python and the required python packages
RUN apt-get -y install python-matplotlib
RUN pip install pillow python-Levenshtein

# Attempting to install Harvards distance module
WORKDIR /
RUN wget http://lstm.seas.harvard.edu/latex/third_party/Distance-0.1.3.tar.gz
RUN tar zxf Distance-0.1.3.tar.gz
WORKDIR /distance
RUN python setup.py install

# Attempting install of tools necessary for PDFLatex
RUN apt-get -y install texlive-latex-base

# Attempting ImageMagick install
# RUN apt-get install -y build-essential checkinstall && apt-get build-dep imagemagick -y
# WORKDIR /
# RUN wget https://www.imagemagick.org/download/ImageMagick.tar.gz
# RUN tar xf ImageMagick.tar.gz
# WORKDIR /ImageMagick-7
# RUN /ImageMagick-7.0.8-23/configure && make
# RUN make install
# RUN ldconfig /usr/local/lib

# RUN checkinstall    # The install instructions said to do this, but I believe those are out of date

# Installing webkit2png
RUN apt-get -y install libwebkit-dev
WORKDIR /usr/local/bin
RUN wget https://raw.githubusercontent.com/paulhammond/webkit2png/master/webkit2png
RUN chmod a+x /usr/local/bin/webkit2png

# Cloning the actual code from Harvard's im2markup repo
WORKDIR /
RUN git clone https://github.com/harvardnlp/im2markup.git
WORKDIR /im2markup

# I didn't really know what else to use as a test command
CMD ["th", "src/train.lua", "-h"]
