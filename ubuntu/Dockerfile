FROM ubuntu

USER root

RUN apt update
RUN apt -y upgrade
RUN apt install -y python3-pip

ENV DEBIAN_FRONTEND=noninteractive
RUN apt install -y openjdk-8-jre

RUN pip3 install -U pip
RUN pip install -U setuptools wheel
RUN pip install pyspark jupyterlab

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
