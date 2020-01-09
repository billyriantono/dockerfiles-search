FROM tiangolo/uwsgi-nginx-flask:python3.6

# Install the package dependencies (this step is separated
# from copying all the source code to avoid having to
# re-install all python packages defined in requirements.txt
# whenever any source code change is made)
COPY app/requirements.txt /app
RUN pip install --no-cache-dir -r /app/requirements.txt

# Install nltk packages
RUN python -m nltk.downloader punkt stopwords
ENV STATIC_PATH /app/news_search/static


COPY ./app /app
