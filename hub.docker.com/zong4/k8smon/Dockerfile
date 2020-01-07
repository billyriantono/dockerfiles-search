FROM zong4/py37:v0.5.2
WORKDIR /mon
COPY *.py ./
USER nobody
ENTRYPOINT ["python"]
CMD ["k8smon.py", "bxr-pro", "bxr-pro"]