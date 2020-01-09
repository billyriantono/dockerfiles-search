FROM neubiaswg5/cellprofiler-base:latest

ADD CP_detect_nuclei.cppipe /cp/CP_detect_nuclei.cppipe

ENTRYPOINT ["cellprofiler", "-c", "-r", "-b", "--do-not-fetch"]
