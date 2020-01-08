FROM rocker/verse:3.6.1

#  $ docker build . -t continuumio/miniconda3:latest -t continuumio/miniconda3:4.5.11
#  $ docker run --rm -it continuumio/miniconda3:latest /bin/bash
#  $ docker push continuumio/miniconda3:latest
#  $ docker push continuumio/miniconda3:4.5.11

# Add some standard R packages that are mising from the rocker distribution
RUN R -e "remotes::install_version('future', repos='http://cran.us.r-project.org', version= '1.14.0', upgrade = 'never' )"
RUN R -e "remotes::install_version('furrr' , repos='http://cran.us.r-project.org', version= '0.1.0' , upgrade = 'never' )"
RUN R -e "remotes::install_version('sinew' , repos='http://cran.us.r-project.org', version= '0.3.8' , upgrade = 'never' )"
RUN R -e "remotes::install_version('plotly', repos='http://cran.us.r-project.org', version= '4.9.0' , upgrade = 'never' )"

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH

RUN apt-get update --fix-missing && \
    apt-get install -y wget bzip2 ca-certificates curl git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-4.5.11-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh && \
    /opt/conda/bin/conda clean -tipsy && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc

ENV TINI_VERSION v0.16.1
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini

ENTRYPOINT [ "/usr/bin/tini", "--" ]
CMD [ "/bin/bash" ]