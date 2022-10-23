FROM debian:11 as base
ENV DEBIAN_FRONTEND=noninteractive
WORKDIR /app/

FROM base as build
RUN apt-get update && apt-get install -y \
        curl &&                          \
    apt-get clean &&                     \
    rm -rf /var/lib/apt/
RUN curl -L                                                                            \
        'https://github.com/Ombi-app/Ombi/releases/latest/download/linux-x64.tar.gz' | \
    tar -xz

FROM base
WORKDIR /app/
COPY --from=build /app/ .
RUN apt-get update && apt-get install -y \
        libicu67 &&                      \
    apt-get clean &&                     \
    rm -rf /var/lib/apt/
COPY docker-entrypoint.sh /usr/local/bin/
RUN useradd -m app
EXPOSE 5000
ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["./Ombi"]
