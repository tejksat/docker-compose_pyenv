ARG CENTOS_VERSION=${CENTOS_VERSION:-"CENTOS_VERSION NOT SET"}

FROM centos:${CENTOS_VERSION}

ARG PYTHON_VERSION=${PYTHON_VERSION:-"PYTHON_VERSION NOT SET"}

# `git` is required for pyenv installer
RUN yum -y install git
RUN curl https://pyenv.run | sh
ENV PATH="/root/.pyenv/bin:$PATH"

# the following packages are required for installing python versions using pyenv
RUN yum -y install gcc make zlib-devel openssl-devel
RUN pyenv install ${PYTHON_VERSION}
RUN pyenv virtualenv ${PYTHON_VERSION} app-context
ENV PATH="/root/.pyenv/versions/app-context/bin:$PATH"

COPY . /app
WORKDIR /app

RUN pip install -r requirements-test.txt

USER 1000
