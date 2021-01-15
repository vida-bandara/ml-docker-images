FROM fedora

USER root

RUN dnf -y install pip
RUN dnf -y install java-1.8.0-openjdk.x86_64 java-1.8.0-openjdk-devel.x86_64

RUN pip install matplotlib pillow
RUN pip install pandas
RUN pip install -f http://h2o-release.s3.amazonaws.com/h2o/latest_stable_Py.html h2o
RUN pip install pyspark
RUN pip install jupyter jupyterlab

RUN jupyter notebook --generate-config
RUN echo "c.NotebookApp.ip = '0.0.0.0'" >> /root/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.allow_root = True" >> /root/.jupyter/jupyter_notebook_config.py
RUN echo "c.NotebookApp.token = ''" >> /root/.jupyter/jupyter_notebook_config.py

ENV PYSPARK_PYTHON=python3
ENV SPARK_HOME=/usr/local/lib/python3.9/site-packages/pyspark
ENV PYSPARK_DRIVER_PYTHON=jupyter
ENV PYSPARK_DRIVER_PYTHON_OPTS='lab'

RUN mkdir /src
RUN mkdir /data

WORKDIR /src
EXPOSE 8888

CMD pyspark
