
# up mysql

``` shell
esdocker-compose up -d

docker exec mysql-slave sh -c "export MYSQL_PWD=password; mysql -u root app -e 'show slave status \G'"

docker exec mysql-master sh -c "export MYSQL_PWD=password; mysql -u root app -e 'create table t (id int not null primary key)'"
docker exec mysql-master sh -c "export MYSQL_PWD=password; mysql -u root app -e 'insert into t values (1)'"

docker exec mysql-slave sh -c "export MYSQL_PWD=password; mysql -u root app -e 'show slave status \G'"

docker exec mysql-slave sh -c "export MYSQL_PWD=password; mysql -u root app -e 'select * from t'"
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
```

