VERSION 0.6

ARG FPM_VERSION=1.14.2

build:
	FROM alpine:latest

	RUN apk --no-cache --update add \
		bzip2 \
		dpkg-dev \
		gzip \
		rpm-dev \
		ruby \
		tar \
		xz \
		zip

	RUN apk --no-cache --update add --virtual .build-deps \
		gcc \
		musl-dev \
		ruby-dev \
		&& gem install fpm --version $FPM_VERSION \
		&& apk del .build-deps

	RUN adduser -h /src -D fpm

	USER fpm
	WORKDIR /src
	CMD ["fpm"]

	SAVE IMAGE fpm:$FPM_VERSION

publish:
	FROM +build
	SAVE IMAGE --push quay.io/zoni/fpm:$FPM_VERSION
	SAVE IMAGE --push quay.io/zoni/fpm:latest
