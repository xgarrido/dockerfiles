FROM ubuntu:16.04
MAINTAINER Xavier Garrido <xavier.garrido@lal.in2p3.fr>

RUN apt-get update && apt-get install -y \
    build-essential                      \
    curl                                 \
    git                                  \
    libbz2-dev                           \
    libglu1-mesa-dev                     \
    libjpeg-dev                          \
    libqt5svg5-dev                       \
    libx11-dev                           \
    libxext-dev                          \
    libxft-dev                           \
    libxpm-dev                           \
    libpng12-dev                         \
    locales                              \
    ruby                                 \
    qt5-default                          \
    subversion                           \
    wget                                 \
    zlib1g-dev                           \
    zsh

RUN locale-gen en_US.UTF-8

RUN useradd -m -U snemo

USER snemo
WORKDIR /home/snemo

# Zsh env.
RUN wget --no-check-certificate https://raw.github.com/xgarrido/dotfiles/master/zshrc -O ~/.zshrc
RUN git clone https://github.com/zsh-users/antigen.git ~/.config/zsh/antigen
RUN /bin/zsh -i ~/.config/zsh/antigen/antigen.zsh update

# SuperNEMO/software
RUN /bin/zsh -i -c "pkgman install --install-dir ~/software brew"
RUN /bin/zsh -i -c "pkgman install --install-dir ~/software bayeux"
RUN /bin/zsh -i -c "pkgman install --install-dir ~/software --falaise-version=SuperNEMO-DBD falaise"
