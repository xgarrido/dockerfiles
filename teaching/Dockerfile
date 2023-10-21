FROM ubuntu:22.04

LABEL maintener="Xavier Garrido <xavier.garrido@universite-paris-saclay.fr>"
LABEL timestamp="Sat Oct 21 19:01:10 CEST 2023"


RUN apt-get update && apt-get install -y \
    emacs                                \
    git                                  \
    imagemagick                          \
    make                                 \
    wget                                 \
    zsh

# Fix pdf conversion policy (see https://stackoverflow.com/questions/52998331/imagemagick-security-policy-pdf-blocking-conversion)
RUN sed -i '/disable ghostscript format types/,+6d' /etc/ImageMagick-6/policy.xml

RUN useradd -m -U teaching
USER teaching
ENV USER teaching
WORKDIR /home/teaching

# Zsh env.
RUN wget --no-check-certificate https://raw.githubusercontent.com/xgarrido/zsh-dotfiles/master/dotfiles/zshrc -O ~/.zshrc
RUN /bin/zsh -i
