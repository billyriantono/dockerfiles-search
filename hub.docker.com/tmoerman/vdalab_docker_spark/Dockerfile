# See https://github.com/jupyter/docker-stacks/tree/master/pyspark-notebook
FROM jupyter/pyspark-notebook
MAINTAINER VDA-LAB

# Add file containing the list of students for this academic year
ADD students_2017.txt students.txt
# Create a directory for each student
RUN cat students.txt | xargs -n 1 mkdir

# Add the exercise notebook
ADD spark_exercises.ipynb spark_exercises.ipynb
# Copy the ipynb template into each of the student folders
RUN cat students.txt | xargs -n 1 cp spark_exercises.ipynb

# Clean up added files
RUN rm students.txt
RUN rm spark_exercises.ipynb

# Add data files
ADD data /usr/local/data

# Set notebook password in jupyter config file
RUN sed -i "/c.NotebookApp.open_browser = False/a c.NotebookApp.token = 'i0u19a'" /home/jovyan/.jupyter/jupyter_notebook_config.py
