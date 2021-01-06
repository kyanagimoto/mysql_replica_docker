
# up mysql

``` shell
docker-compose up -d

docker-compose exec mysql-replica mysql -e 'show slave status \G'


docker-compose exec mysql-primary mysql test -e 'create table t (id int not null primary key)'
docker-compose exec mysql-primey mysql test -e 'insert into t values (1)'

docker-compose exec mysql-replica mysql -e 'show slave status \G'

docker-compose exec mysql-replica mysql test -e 'select * from t'
```

# rails new

``` shell
bundle init

bundle install

export LIBRARY_PATH=$LIBRARY_PATH:/usr/local/opt/openssl/lib/

bundle exec rails new . -d mysql

# config/database.yml
# ec app/models/application_record.rb
# ec config/application.rb

bundle exec rails generate scaffold User name:string email:string

bundle exec rake db:migrate

# mysql -h 0.0.0.0 -u root -v mysql -P 13306 test
# show columns from users;

be rails s

docker-compose stop mysql-replica
docker-compose restart mysql-replica

docker-compose stop mysql-primary
docker-compose start mysql-primary
```

