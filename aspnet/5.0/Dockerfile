FROM martinussuherman/alpine-tz-ep:dev-glibc

ENV \
    # container/su-exec UID \
    EUID=1001 \
    # container/su-exec GID \
    EGID=1001 \
    # container/su-exec user name \
    EUSER=docker-user \
    # container/su-exec group name \
    EGROUP=docker-group \
    # container user home dir \
    EHOME= \
    # should user home dir get chown'ed? (yes/no) \
    ECHOWNHOME=no \
    # additional directories to create + chown (space separated) \
    ECHOWNDIRS= \
    # additional files to create + chown (space separated) \
    ECHOWNFILES= \
    # container timezone \
    TZ=UTC 

RUN apk --no-cache --update add \
    ca-certificates \
    \
    # .NET Core dependencies
    icu-libs \
    krb5-libs \
    libgcc \
    libintl \
    libssl1.1 \
    libstdc++ \ 
    lttng-ust \
    numactl \
    zlib

# Install ASP.NET Core
ENV ASPNET_VERSION=5.0.2

RUN wget -O aspnetcore.tar.gz https://dotnetcli.azureedge.net/dotnet/aspnetcore/Runtime/$ASPNET_VERSION/aspnetcore-runtime-$ASPNET_VERSION-linux-musl-x64.tar.gz \
    && aspnetcore_sha512='d9582bee1dc513288d386ee52bdeb9ed4d5d191d6843b68773f7979ea0d0527c35599722d700a33ce9d59752b44666b17ab7bb36da169c180965252a2742174c' \
    && echo "$aspnetcore_sha512  aspnetcore.tar.gz" | sha512sum -c - \
    && mkdir -p /usr/share/dotnet \
    && tar -oxzf aspnetcore.tar.gz -C /usr/share/dotnet \
    && ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet \
    && rm aspnetcore.tar.gz
