FROM konmeo/python3

MAINTAINER konmeo

RUN install_packages libfreetype6 libpng16-16 liblapack3
RUN pip3 install --no-cache-dir \
    	cython numpy pandas matplotlib plotly bokeh tables \
        scipy scikit-learn keras tensorflow
