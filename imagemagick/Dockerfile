FROM ubuntu:bionic
RUN sed -Ei 's/^# deb-src/deb-src/' /etc/apt/sources.list
RUN apt-get update -y
RUN apt-get build-dep -y imagemagick
RUN apt-get install -y checkinstall libwebp-dev libopenjp2-7-dev librsvg2-dev \
libde265-dev libheif-dev
RUN apt-get install -y wget
RUN mkdir $HOME/imagemagick_build && cd $HOME/imagemagick_build && \
wget https://www.imagemagick.org/download/ImageMagick-7.0.8-11.tar.bz2 && \
tar xvf ImageMagick-7.0.8-11.tar.bz2 && cd ImageMagick-7.0.8-11 && \
./configure --with-rsvg && make && \
checkinstall -D --install=yes --fstrans=no --pakdir "$HOME/imagemagick_build" \
     --pkgname imagemagick --backup=no --deldoc=yes --deldesc=yes --delspec=yes --default \
     --pkgversion "7.0.8-11" && \
make distclean && ldconfig
ENTRYPOINT ["convert"]
