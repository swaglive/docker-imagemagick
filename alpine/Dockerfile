FROM        alpine:3.16

ARG         version=7.1.0-37
ARG         MAKEFLAGS="-j4"

ENTRYPOINT  ["convert"]

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
                libde265-dev \
                build-base && \
            curl -sL https://github.com/ImageMagick/ImageMagick/archive/refs/tags/${version}.tar.gz | tar xz && \
            cd ImageMagick-${version} && \
            ./configure \
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
            make install && \
            rm -rf ../ImageMagick-${version} && \
            apk add --virtual .run-deps \
                zlib \
                zstd \
                libheif \
                libde265 \
                libwebp \
                jpeg \
                xz \
                librsvg-dev \
                libpng \
                tiff \
                msttcorefonts-installer \
                fontconfig \
                libzip && \
            apk del .build-deps
