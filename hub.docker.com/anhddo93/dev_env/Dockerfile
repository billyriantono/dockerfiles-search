FROM anhddo93/dev_env:v5

RUN pip3 install ipdb seaborn cvxopt
EXPOSE 8050 8888
CMD ["jupyter", "lab", "--port=8888", "--ip=0.0.0.0", "--no-browser", "--allow-root"]
