FROM centos:7
MAINTAINER Xavier Garrido <xavier.garrido@lal.in2p3.fr>

RUN yum -y update && yum install -y \
    atlas-devel                     \
    blas-devel                      \
    bzip2                           \
    gcc-c++                         \
    gcc-gfortran                    \
    git                             \
    lapack-devel                    \
    ncurses-devel                   \
    make                            \
    python-devel                    \
    tkinter                         \
    which                           \
    wget

# Install MKL
RUN rpm --import https://yum.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS-2019.PUB
RUN yum-config-manager --add-repo https://yum.repos.intel.com/mkl/setup/intel-mkl.repo && yum install -y intel-mkl-2018.2-046

# Install decent version of zsh
RUN zsh_version=5.3.1; wget http://sourceforge.net/projects/zsh/files/zsh/${zsh_version}/zsh-${zsh_version}.tar.gz && \
    tar xzvf zsh-${zsh_version}.tar.gz && cd zsh-${zsh_version} && ./configure --without-tcsetpgrp && make && make install && \
    ln -sf /usr/local/bin/zsh /bin/zsh

# Add CMB user
RUN useradd -m -U cmb
USER cmb
ENV USER cmb
WORKDIR /home/cmb

# Zsh env.
RUN wget --no-check-certificate https://raw.github.com/xgarrido/dotfiles/master/zshrc -O ~/.zshrc
RUN git clone https://github.com/zsh-users/antigen.git ~/.config/zsh/antigen
RUN /bin/zsh -i -c "antigen update; antigen reset"

# CMB/software
# RUN /bin/zsh -i -c "pkgman install --install-dir ~/software @cmb"
RUN /bin/zsh -i -c "pkgman install --install-dir ~/software python2"
RUN /bin/zsh -i -c "pkgman install --install-dir ~/software pypico --without-data"
RUN /bin/zsh -i -c "pkgman install --install-dir ~/software cmt"
RUN /bin/zsh -i -c "pkgman install --install-dir ~/software class"
RUN /bin/zsh -i -c "pkgman install --install-dir ~/software cfitsio"
RUN /bin/zsh -i -c "pkgman install --install-dir ~/software planck --without-data"
RUN /bin/zsh -i -c "pkgman install --install-dir ~/software camel --without-data"
