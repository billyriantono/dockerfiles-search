FROM php:7-fpm
FROM bash:4.4
USER root
ADD file1.py /
ADD file2.py /
ADD grader.sh /
CMD ["bash", "chmod +x file1.py"]
CMD ["bash", "chmod +x file2.py"]
CMD ["bash", "/grader.sh"]
