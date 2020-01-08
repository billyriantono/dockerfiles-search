FROM debian:latest

ENV working_dir /app

WORKDIR ${working_dir}
  
RUN apt-get update && \
    apt-get install git -y 
ENTRYPOINT ["git"] 
