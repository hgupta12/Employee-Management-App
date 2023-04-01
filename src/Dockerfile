FROM ruby:3.0.5

RUN curl -sL https://deb.nodesource.com/setup_16.x -o /tmp/nodesource_setup.sh 
RUN bash /tmp/nodesource_setup.sh

RUN apt-get update && apt-get -y upgrade && apt-get -y install \
    nodejs \
    default-libmysqlclient-dev \
    imagemagick \
    default-mysql-client \
    libmagickcore-dev \
    libmagickwand-dev

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | gpg --dearmor | tee /etc/apt/trusted.gpg.d/yarn.gpg
RUN echo "deb [signed-by=/etc/apt/trusted.gpg.d/yarn.gpg] https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt update && apt install yarn

RUN rm -rf /var/lib/apt/lists/*

RUN gem install bundler

WORKDIR /app

COPY . /app
COPY Gemfile Gemfile.lock ./

RUN bundle install

RUN bundle exec rails assets:precompile

# RUN bundle exec rails db:migrate

EXPOSE 8080

CMD rm -f tmp/pids/server.pid && rails s -b '0.0.0.0'