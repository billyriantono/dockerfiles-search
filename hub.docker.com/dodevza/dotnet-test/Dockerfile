FROM microsoft/dotnet:2.1-sdk

ENV WORKING_FOLDER /context
ENV RESULTS_DIRECTORY /results_directory
ENV CONFIGURATION Debug
ENV PROJECT ""
ENV FILTER ""

RUN mkdir $RESULTS_DIRECTORY

WORKDIR $WORKING_FOLDER

#Map the context path the project will run from
VOLUME $WORKING_FOLDER

#Map the path the test results will be populated to
VOLUME $RESULTS_DIRECTORY


ENTRYPOINT dotnet test "$PROJECT" -c "$CONFIGURATION" --filter "$FILTER" -r "$RESULTS_DIRECTORY"