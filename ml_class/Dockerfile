FROM python:2.7

MAINTAINER Tony Hariman <thariman@gmail.com>

RUN  apt-get update && apt-get install -y \
     wget \
     unzip

RUN   pip install --no-cache-dir nltk          && \
      pip install --no-cache-dir numpy         && \
      pip install --no-cache-dir hcluster

RUN  wget --quiet "http://bonsai.hgc.jp/~mdehoon/software/cluster/Pycluster-1.52.tar.gz" && \
     tar -xzf Pycluster-1.52.tar.gz                                                      && \
     cd Pycluster-1.52                                                                   && \
     python setup.py install                                                             && \
     cd ..                                                                               && \
     rm -rf /root/Pycluster-1.52 /root/Pycluster-1.52.tar.gz

RUN  wget --quiet "https://raw.githubusercontent.com/nltk/nltk_data/gh-pages/packages/tokenizers/punkt.zip" && \
     mkdir -p /root/nltk_data/tokenizers                                                                    && \
     unzip punkt.zip -d /root/nltk_data/tokenizers/                                                         && \
     rm -rf punkt.zip

WORKDIR /root

# Code for O'reilly Hilary Mason: An Introduction to Machine Learning with Web Data'
RUN  git clone https://github.com/hmason/ml_class.git


# cleanup
RUN   apt-get remove -y libncurses5-dev                                   && \
      apt-get autoremove -y                                               && \
      apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*



CMD [ "/bin/bash" ]
