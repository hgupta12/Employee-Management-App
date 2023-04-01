FROM ruby:3.0.5-alpine

RUN apk add --update \
    build-base \
    mariadb-dev \
    sqlite-dev \
    nodejs \
    yarn \
    tzdata \
    && rm -rf /var/cache/apk/*

RUN gem install bundler

WORKDIR /app

COPY . /app
COPY Gemfile Gemfile.lock ./

RUN bundle install

RUN bundle exec rails assets:precompile

# RUN bundle exec rails db:migrate

EXPOSE 3000

CMD rm -f tmp/pids/server.pid && rails s -b '0.0.0.0'