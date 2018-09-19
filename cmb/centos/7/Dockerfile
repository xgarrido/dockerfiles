FROM centos:7
MAINTAINER Xavier Garrido <xavier.garrido@lal.in2p3.fr>

RUN yum -y update && yum install -y \
    blas-devel                      \
    gcc-c++                         \
    gcc-gfortran                    \
    git                             \
    lapack-devel                    \
    ncurses-devel                   \
    make                            \
    python-devel                    \
    tkinter                         \
    wget

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
RUN /bin/zsh -i ~/.config/zsh/antigen/antigen.zsh update


# CMB/software
RUN /bin/zsh -i -c "pkgman install --install-dir ~/software python2"
RUN /bin/zsh -i -c "pkgman install --install-dir ~/software cmt"
RUN /bin/zsh -i -c "pkgman install --install-dir ~/software class"
RUN /bin/zsh -i -c "pkgman install --install-dir ~/software pypico"
RUN /bin/zsh -i -c "pkgman install --install-dir ~/software planck"
RUN /bin/zsh -i -c "pkgman install --install-dir ~/software camel"
