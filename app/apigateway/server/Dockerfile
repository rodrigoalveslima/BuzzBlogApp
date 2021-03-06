# Copyright (C) 2020 Georgia Tech Center for Experimental Research in Computer
# Systems

# Define base configuration.
FROM ubuntu:20.04
MAINTAINER ral@gatech.edu
WORKDIR /opt/BuzzBlogApp/app/apigateway/service/server

# Install software dependencies.
RUN apt-get update \
  && DEBIAN_FRONTEND=noninteractive apt-get install -y \
    python3-pip
RUN pip3 install --no-cache-dir uWSGI==2.0.19.1 && \
    pip3 install --no-cache-dir Flask-HTTPAuth==4.2.0 && \
    pip3 install --no-cache-dir PyYaml==5.3.1 && \
    pip3 install --no-cache-dir spdlog==2.0.4 && \
    pip3 install --no-cache-dir thrift==0.13.0

# Copy service client libraries.
COPY site-packages site-packages

# Copy source code.
COPY src src

# Start the server.
CMD ["/bin/bash", "-c", "PYTHONPATH=/opt/BuzzBlogApp/app/apigateway/service/server/site-packages uwsgi --ini /etc/uwsgi/uwsgi.ini --wsgi-file src/apigateway.py --callable app"]
