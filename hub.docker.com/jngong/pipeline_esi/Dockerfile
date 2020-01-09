#Docker Build file to create the runtime-matlab-2016b with pipelineESI image by NeuroScience Center Cuba
from mcin/matlab-runtime:R2017b
MAINTAINER Jinnan Gong <gongjinnan1989@gmail.com>

WORKDIR /media
ADD PipelineESI /media/PipelineESI
RUN chmod 777 -R /media/PipelineESI/
ENV PATH=$PATH:/media/PipelineESI/
WORKDIR /media/PipelineESI/
ENTRYPOINT ["/media/PipelineESI/pipeline_brainstorm_fs"]
