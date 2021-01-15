FROM ubuntu

USER root

RUN apt update
RUN apt -y upgrade
RUN apt -y install python3 python3-pip

RUN export DEBIAN_FRONTEND=noninteractive DEBCONF_NONINTERACTIVE_SEEN=true; \
    echo "tzdata tzdata/Areas select America" >> /tmp/preseed.txt; \
    echo "tzdata tzdata/Zones/Europe select Chicago" >> /tmp/preseed.txt; \
    debconf-set-selections /tmp/preseed.txt; \
    apt -y install openjdk-8-jdk

RUN pip3 install matplotlib pillow
RUN pip3 install pandas
RUN pip3 install -f http://h2o-release.s3.amazonaws.com/h2o/latest_stable_Py.html h2o
RUN pip3 install pyspark
RUN pip3 install jupyter jupyterlab

RUN jupyter notebook --generate-config
RUN echo "c.NotebookApp.ip = '0.0.0.0'" >> /root/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.allow_root = True" >> /root/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.token = ''" >> /root/.jupyter/jupyter_notebook_config.py

ENV PYSPARK_PYTHON=python3
ENV SPARK_HOME=/usr/local/lib/python3.8/dist-packages/pyspark
ENV PYSPARK_DRIVER_PYTHON=jupyter
ENV PYSPARK_DRIVER_PYTHON_OPTS='lab'

RUN mkdir /src
RUN mkdir /data

WORKDIR /src
EXPOSE 8888

CMD pyspark
