FROM centos:8

USER root

RUN yum -y update
RUN yum -y install yum-utils
RUN yum -y groupinstall development
RUN yum -y install python3
RUN yum -y install java-1.8.0-openjdk java-1.8.0-openjdk-devel

RUN pip3 install matplotlib pillow
RUN pip3 install pandas
RUN pip3 install -f http://h2o-release.s3.amazonaws.com/h2o/latest_stable_Py.html h2o
RUN pip3 install pyspark
RUN pip3 install jupyter jupyterlab

# RUN jupyter notebook --generate-config
# RUN echo "c.NotebookApp.ip = '0.0.0.0'" >> /root/.jupyter/jupyter_notebook_config.py
# RUN echo "c.NotebookApp.allow_root = True" >> /root/.jupyter/jupyter_notebook_config.py
# RUN echo "c.NotebookApp.token = ''" >> /root/.jupyter/jupyter_notebook_config.py

RUN jupyter server --generate-config
RUN echo "c.NotebookApp.ip = '0.0.0.0'" >> /root/.jupyter/jupyter_server_config.py
RUN echo "c.NotebookApp.allow_root = True" >> /root/.jupyter/jupyter_server_config.py
RUN echo "c.NotebookApp.token = ''" >> /root/.jupyter/jupyter_server_config.py

ENV PYSPARK_PYTHON=python3
ENV SPARK_HOME=/usr/local/lib/python3.6/site-packages/pyspark
ENV PYSPARK_DRIVER_PYTHON=jupyter
ENV PYSPARK_DRIVER_PYTHON_OPTS='lab'

RUN mkdir /src
RUN mkdir /data

WORKDIR /src
EXPOSE 8888

CMD pyspark
