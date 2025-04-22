# ---------------------------------------------
# Overleaf TexLive Base (ayaka-notes/overleaf)
# ---------------------------------------------

# ---------------------------------------------
# How to pull? 
# $ docker pull ghcr.io/ayaka-notes/texlive-full:base
# How to build?
# $ docker build -t ghcr.io/ayaka-notes/texlive-full:base ./texlive/Base
# ---------------------------------------------

# This Dockerfile is used to build texlive-full:base
# And texlive:2024, texlive:2023 and so on are all based on this
# Base Image Contain fonts, apt-installed component
FROM ubuntu:22.04

# LABEL
# -----------------------------------
LABEL \
    org.opencontainers.image.title="Docker Image of TeXLive" \
    org.opencontainers.image.authors="ayaka-notes <public@ayaka.space>" \
    org.opencontainers.image.source="https://github.com/ayaka-notes/texlive-full" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.description="Overleaf TeXLive Image by ayaka-notes"

# Makes sure LuaTex cache is writable
# -----------------------------------
ENV TEXMFVAR=/tmp/texmf-var

# Set ENV to noninteractive
# -----------------------------------
ENV DEBIAN_FRONTEND noninteractive

# Update to ensure dependencies are updated
# ------------------------------------------
ENV REBUILT_AFTER="2024-14-02"

# Install dependencies
# --------------------
RUN apt-get update && apt-get install -y --no-install-recommends \
    fontconfig inkscape pandoc python3-pygments wget python3 \
    gnupg gnuplot perl-modules perl ca-certificates git ghostscript \
    freeglut3-dev libgdal-dev libfftw3-double3 libfftw3-long3 libfftw3-single3 \
    chktex culmus culmus-fancy default-jdk-headless dot2tex graphviz gsfonts \
    imagemagick libcurl4 libexpat1 libfontconfig libfreetype6 libgsl27 libidn12 \
    libijs-0.35 libjbig2dec0 libjpeg8 liblcms2-2 libmagick++-6.q16-8 libncurses6 \
    libopenjp2-7 libosmesa6 libpaper1 libpng16-16 libtiff5 libudunits2-0 libxml2 \
    python-is-python3 python3-numpy python3-pygments python3-scipy python3-simpy \
    strace t1-cyrillic time zlib1g \
    qpdf r-base-core tar make \
    && rm -rf /var/lib/apt/lists/*


# Install Extra fonts
COPY ./extrafonts /usr/share/fonts/


# Install fonts
# --------------------
RUN echo "ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true" | debconf-set-selections \
&& apt-get update && apt-get install -y ttf-mscorefonts-installer ttf-bitstream-vera \
&& apt update && apt search ^fonts | grep -o '^fonts[^/]*' | xargs apt install -y \
&& rm -rf /var/lib/apt/lists/* \
&& fc-cache -f 
