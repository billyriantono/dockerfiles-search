FROM jupyter/scipy-notebook

RUN pip install \
        bokeh \
        holoviews \
        panoptes-client \
        panoptescli \
        panoptes-aggregation

CMD jupyter notebook --ip='0.0.0.0' --port=8888 --no-browser --allow-root
