FROM python
RUN pip install Flask
COPY rng.py /
CMD ["python", "rng.py"]
EXPOSE 8080
LABEL io.openshift.expose-services "8080:http" io.k8s.display-name="dockercoins RNG service"
