FROM ubuntu:16.04
MAINTAINER Xavier Garrido <xavier.garrido@lal.in2p3.fr>

RUN apt-get update && apt-get install -y \
    build-essential                      \
    git                                  \
    wget                                 \
    zsh

RUN locale-gen en_US.UTF-8

RUN useradd -m -U cmb
USER cmb
ENV USER cmb
WORKDIR /home/cmb

# Zsh env.
RUN wget --no-check-certificate https://raw.github.com/xgarrido/dotfiles/master/zshrc -O ~/.zshrc
RUN git clone https://github.com/zsh-users/antigen.git ~/.config/zsh/antigen
RUN /bin/zsh -i ~/.config/zsh/antigen/antigen.zsh update

# SuperNEMO/software
RUN /bin/zsh -i -c "pkgman install --install-dir ~/software python2"
