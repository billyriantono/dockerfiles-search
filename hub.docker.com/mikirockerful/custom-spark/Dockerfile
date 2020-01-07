FROM gettyimages/spark:2.2.0-hadoop-2.7

# Copy the JAR
COPY ./recommender_command_line.jar /usr/spark-2.2.0/

# Download the dataset
RUN curl https://storage.googleapis.com/aas-data-sets/profiledata_06-May-2005.tar.gz --output "profiledata_06-May-2005.tar.gz" && tar -xvzf profiledata_06-May-2005.tar.gz;head -n 10000 ./profiledata_06-May-2005/user_artist_data.txt > ./profiledata_06-May-2005/user_artist_data_10000.txt;mkdir /usr/spark-2.2.0/datasetFiles;mv ./profiledata_06-May-2005/* /usr/spark-2.2.0/datasetFiles