FROM        alpine:3.16 as imagemagick

ARG         version=7.1.0-37
ARG         MAKEFLAGS="-j4"

RUN         apk add --virtual .build-deps \
                curl \
                zlib-dev \
                zstd-dev \
                libheif-dev \
                libwebp-dev \
                jpeg-dev \
                xz-dev \
                librsvg-dev \
                libpng-dev \
                tiff-dev \
                msttcorefonts-installer \
                fontconfig \
                libzip-dev \
                build-base && \
            curl -sL https://github.com/ImageMagick/ImageMagick/archive/refs/tags/${version}.tar.gz | tar xz

WORKDIR     ImageMagick-${version}

RUN         ./configure \
                --with-bzlib=yes \
                --with-fontconfig=yes \
                --with-freetype=yes \
                --with-heic=yes \
                --with-jpeg=yes \
                --with-lzma=yes \
                --with-magick-plus-plus=yes \
                --with-png=yes \
                --with-rsvg=yes \
                --with-tiff=yes \
                --with-webp=yes \
                --with-x=yes \
                --with-zip=yes \
                --with-zlib=yes \
                --with-zstd=yes && \
            make && \
            make install

###

FROM        alpine:3.16

ENTRYPOINT  ["convert"]

COPY        --from=imagemagick /usr/local/bin /usr/local/bin
COPY        --from=imagemagick /usr/local/include /usr/local/include