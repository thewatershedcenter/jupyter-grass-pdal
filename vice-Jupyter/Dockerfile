FROM harbor.cyverse.org/vice/jupyterlab/geospatial:2.2.9

USER root

# onstall pdal
RUN conda install -y -c conda-forge \
    laz-perf=2.1.0 \
    pdal=2.3.0 \
    python-pdal=2.4.2 

# define versions to be used
ARG PDAL_VERSION=2.3.0

SHELL ["/bin/bash", "-c"]

WORKDIR /tmp

RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y --no-install-recommends --no-install-suggests \
    build-essential \
    bison \
    bzip2 \
    cmake \
    curl \
    flex \
    g++ \
    gcc \
    gdal-bin \
    git \
    grass \
    language-pack-en-base \
    libbz2-dev \
    libcairo2 \
    libcairo2-dev \
    libcurl4-gnutls-dev \
    libfftw3-bin \
    libfftw3-dev \
    libfreetype6-dev \
    libgdal-dev \
    libgeos-dev \
    libgsl0-dev \
    libjpeg-dev \
    libjsoncpp-dev \
    libnetcdf-dev \
    libncurses5-dev \
    libopenblas-base \
    libopenblas-dev \
    libopenjp2-7 \
    libopenjp2-7-dev \
    libpnglite-dev \
    libpq-dev \
    libproj-dev \
    libpython3-all-dev \
    libsqlite3-dev \
    libtiff-dev \
    libzstd-dev \
    locales \
    make \
    mesa-common-dev \
    moreutils \
    ncurses-bin \
    netcdf-bin \
    proj-bin \
    proj-data \
    software-properties-common \
    sqlite3 \
    subversion \
    unzip \
    vim \
    wget \
    zip \
    zlib1g-dev

RUN echo LANG="en_US.UTF-8" > /etc/default/locale
RUN echo en_US.UTF-8 UTF-8 >> /etc/locale.gen && locale-gen

# Install the Dask dashboard
RUN pip install --quiet --no-cache-dir dask-labextension && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

WORKDIR /root/work/

# Dask Scheduler & Bokeh ports
EXPOSE 8787
EXPOSE 8786

ENTRYPOINT ["jupyter", "lab", "--ip=0.0.0.0", "--allow-root"]