FROM postgres:16.4
# default env is US, but can be changed
ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en\
    LC_ALL=en_US.UTF-8

RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y postgresql-16-cron postgresql-plpython3-16 \
    locales \
    apt-utils \
    bash-completion \
    && \
    sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8 && \
    echo "## enable pg_cron as shared lib\n"\
    "shared_preload_libraries = 'pg_cron'\n"\
    "##make default database to contain the cron tables to avoid chicken and egg problem\n"\
    "cron.database_name = 'postgres'\n" >> /usr/share/postgresql/postgresql.conf.sample

# add the helper/utilities to the path.
COPY usr/local/bin /usr/local/bin
