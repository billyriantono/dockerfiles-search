FROM microsoft/azure-cli:2.0.58

COPY ./file.sh / 
RUN chmod +x /file.sh 

ENTRYPOINT ["/file.sh"]

CMD ["bash"]