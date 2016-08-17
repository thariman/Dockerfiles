FROM golang:1.6

MAINTAINER Tony Hariman <thariman@gmail.com>

COPY  sources.list /etc/apt/sources.list

RUN   apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 9DBB0BE9366964F134855E2255F96FCF8231B6DD   && \
      echo "deb http://ppa.launchpad.net/neovim-ppa/unstable/ubuntu wily main" >> /etc/apt/sources.list.d/neovim.list     && \
      echo "deb-src http://ppa.launchpad.net/neovim-ppa/unstable/ubuntu wily main" >> /etc/apt/sources.list.d/neovim.list && \
      apt-get update && apt-get install -y \
      less \
      neovim

RUN   update-alternatives --install /usr/bin/vi vi /usr/bin/nvim 60         && \
      update-alternatives --install /usr/bin/vim vim /usr/bin/nvim 60       && \
      update-alternatives --install /usr/bin/editor editor /usr/bin/nvim 60 

# add dev user
RUN   adduser dev --disabled-password --gecos ""                          && \
      echo "ALL            ALL = (ALL) NOPASSWD: ALL" >> /etc/sudoers     && \
      chown -R dev:dev /home/dev /go                                      && \
# cleanup
      apt-get remove -y ncurses-dev                                       && \
      apt-get autoremove -y                                               && \
      apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

USER dev
ENV HOME /home/dev
WORKDIR	$HOME

RUN  git clone --recursive https://github.com/jfrazelle/.vim.git .vim && \
     ln -sf $HOME/.vim/vimrc $HOME/.vimrc                             && \
     mkdir -p ${XDG_CONFIG_HOME:=$HOME/.config}                       && \
     ln -snf "$HOME/.vim" $XDG_CONFIG_HOME/nvim                       && \
     ln -snf "$HOME/.vimrc" $XDG_CONFIG_HOME/nvim/init.vim
