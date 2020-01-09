FROM ottov/genomicsdb-s3-ecs:latest
MAINTAINER Otto Valladares <ottov.upenn@gmail.com>

# update OS
RUN apt-get update && \
    apt-get upgrade -y  && \
    apt-get install -y openjdk-8-jre-headless && \
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/*

COPY ./GenomeAnalysis*.jar ./picard-1.130.jar ./run_pipeline.py /


ENTRYPOINT ["python","-u", "run_pipeline.py"]
