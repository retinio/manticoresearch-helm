FROM manticoresearch/manticore:6.3.0

ARG DEBIAN_FRONTEND=noninteractive

# install UK lemmatizer from APT repository
RUN cd ~ \
    && wget https://repo.manticoresearch.com/manticore-repo.noarch.deb \
    && dpkg -i manticore-repo.noarch.deb \
    && apt-get -y update \
    && apt-get -y install manticore-lemmatizer-uk

# install packages needed for building Python
RUN apt-get -y update \
    && apt-get -y install wget build-essential libreadline-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev zlib1g-dev \
    && rm -rf /var/lib/apt/lists/*

# download, build and install Python 3.9 
RUN cd ~ \ 
    && wget https://www.python.org/ftp/python/3.9.4/Python-3.9.4.tgz \
    && tar xzf Python-3.9.4.tgz \
    && cd Python-3.9.4 \
    && ./configure --enable-optimizations --enable-shared \
    && make -j8 altinstall \
    && ldconfig

# install pymorphy2 and UK dictionary
RUN pip3.9 install pymorphy2[fast] \
    && pip3.9 install pymorphy2-dicts-uk
 