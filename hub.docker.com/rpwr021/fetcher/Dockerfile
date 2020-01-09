#base
FROM p7hb/docker-spark

# Update the image to the latest packages
RUN apt-get update


RUN wget https://github.com/rpwr021/fetcher/blob/master/SparkApp.tgz?raw=true -O SparkApp.tgz
RUN tar -xvzf SparkApp.tgz
RUN echo " " >  /root/output/output.txt
RUN echo "bash /root/app/generator.sh 100 /root/input/ /root/data/data2.csv &" >> /root/runapp.sh
RUN echo "spark-submit /root/app/RFP.py /root/input/ /root/output/output.txt 10" >> /root/runapp.sh
RUN chmod +x /root/runapp.sh 

EXPOSE 4040 
EXPOSE 8181

CMD ["/bin/bash", "-c", "/root/runapp.sh server.log 2>&1"]

ENTRYPOINT "/root/runapp.sh" && /bin/bash
