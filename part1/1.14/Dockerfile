FROM ruby:2.6.0

COPY rails-example-project /mydir/rails-example-project  
WORKDIR /mydir/rails-example-project  
RUN apt-get update && apt-get install -y nodejs
RUN gem install bundler
RUN bundle install
RUN rails db:migrate

CMD rails s
