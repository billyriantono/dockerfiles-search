# automatically generated: 2019-12-13T13:58:13.326261
FROM agpipeline/rgb-plot-base-image:1.1
LABEL maintainer="Unknown <>"

COPY requirements.txt packages.txt /home/extractor/

USER root

RUN [ -s /home/extractor/packages.txt ] && \
    (echo "Installing packages" && \
        apt-get update && \
       cat /home/extractor/packages.txt | xargs apt-get install -y --no-install-recommends && \
        rm /home/extractor/packages.txt && \
        apt-get install python3 && \
        apt-get autoremove -y && \
        apt-get clean && \
        rm -rf /var/lib/apt/lists/*) || \
    (echo "No packages to install" && \
        rm /home/extractor/packages.txt)

RUN [ -s /home/extractor/requirements.txt ] && \
    (echo "Install python modules" && \
    python3 -m pip install -U --no-cache-dir pip && \
    python3 -m pip install --no-cache-dir setuptools && \
     python3 -m pip install --no-cache-dir -r /home/extractor/requirements.txt && \
     rm /home/extractor/requirements.txt) || \
    (echo "No python modules to install" && \
     rm /home/extractor/requirements.txt)

COPY model /home/extractor/
RUN mkdir /home/extractor/model/ && \
    chmod a+r /home/extractor/model/
USER extractor
COPY algorithm_rgb.py /home/extractor/
