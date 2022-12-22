
FROM ruby:3.1.3-slim

RUN apt-get update -qq && apt-get install -yq --no-install-recommends \
    build-essential \
    gnupg2 \
    less \
    git \
    libpq-dev \
    postgresql-client \
    libvips42 \
    vim \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV LANG=C.UTF-8 \
  BUNDLE_JOBS=4 \
  BUNDLE_RETRY=3

RUN gem update --system && gem install bundler

WORKDIR /usr/src/app
COPY Gemfile Gemfile.lock ./
RUN bundle check || bundle install --jobs 4

# NOTE: No entrypoint.sh, No CMD and EXPOSE here. Use docker-compose.yml to start rails server or bundle exec sidekiq.