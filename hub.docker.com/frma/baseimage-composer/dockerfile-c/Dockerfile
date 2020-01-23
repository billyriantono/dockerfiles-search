FROM continuumio/miniconda

RUN apt update && apt install git make g++ libgl1-mesa-glx -y
RUN git clone https://github.com/iris-edu/ispaq.git
RUN cd ispaq &&\
#	conda install -c conda-forge readline=6.2 -c r -c r-old -c bioconda --file ispaq-conda-install.txt
    conda install -c conda-forge --file ispaq-conda-install.txt

RUN R CMD INSTALL /ispaq/seismicRoll_1.1.3.tar.gz &&\
	R CMD INSTALL /ispaq/IRISSeismic_1.4.9.tar.gz &&\
	R CMD INSTALL /ispaq/IRISMustangMetrics_2.2.0.tar.gz 

#hack to allow it to read SDS archive file names that have the ".D." in the middle
RUN sed -i "s?fpattern1 = '%s.%s'?fpattern1 = '%s.D.%s'?g" /ispaq/ispaq/concierge.py

#hack to allow saving images to png files
RUN echo "import matplotlib" >> /ispaq/ispaq/PDF_aggregator.py
RUN echo "matplotlib.use('Agg')" >> /ispaq/ispaq/PDF_aggregator.py
# docker run -it --rm --name ispaq -v c:\nmx\pegasus\horizon\ispaq-working:/data ispaq
# python /ispaq/run_ispaq.py -M num_gaps -S "*.*.*.*" --dataselect_url /data
# python /ispaq/run_ispaq.py -M percent_availability -S "*.*.*.*" --sncl_format N.S.L.C.Quality.Year.JulianDay --starttime 2019-300 --endtime 2019-365 --dataselect_url /data
# python /ispaq/run_ispaq.py -M psd_corrected,pdf -S "*.*.*.*" --sncl_format N.S.L.C.Quality.Year.JulianDay --starttime 2019-307 --endtime 2019-308 --dataselect_url /data --station_url /data/NN.SSSSS_20191101T150245Z-fixed.xml --resp_dir /data --pdf_type plot
# python /ispaq/run_ispaq.py -M psd_corrected,pdf -S "*.*.*.*" --sncl_format N.S.L.C.Quality.Year.JulianDay --starttime 2019-305 --endtime 2019-308 --dataselect_url /data --resp_dir /data --pdf_type plot --pdf_interval daily --plot_include legend,colorbar,fixed_axis_limits