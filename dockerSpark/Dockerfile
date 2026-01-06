FROM python:3.11-slim-bookworm

RUN apt-get update && apt-get install -y --no-install-recommends \
    openjdk-17-jdk-headless \
    curl \
    procps \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# To avoid the No such file or directory error regardless of your computer's chip (Intel vs M1/M2), update your Dockerfile to create a "symlink." This makes the path predictable.
RUN ln -s $(readlink -f /usr/bin/java | sed "s:bin/java::") /usr/lib/jvm/java-17-fixed
ENV JAVA_HOME=/usr/lib/jvm/java-17-fixed
ENV SPARK_VERSION=3.5.0
ENV HADOOP_VERSION=3
ENV SPARK_HOME=/opt/spark

RUN curl -sL "https://archive.apache.org/dist/spark/spark-$SPARK_VERSION/spark-$SPARK_VERSION-bin-hadoop$HADOOP_VERSION.tgz" | tar -xz -C /opt && \
    mv /opt/spark-$SPARK_VERSION-bin-hadoop$HADOOP_VERSION $SPARK_HOME

ENV PATH=$PATH:$SPARK_HOME/bin

WORKDIR $SPARK_HOME