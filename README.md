# Airflow-setup-ubuntu
Installation of Airflow in ubuntu server - full detailed steps

sudo apt-get update

export LC_ALL="en_US.UTF-8"
export LC_CTYPE="en_US.UTF-8"
sudo dpkg-reconfigure locales

sudo apt-get install python-setuptools

sudo apt-get install python-pip

sudo pip install --upgrade pip

sudo su postgres
psql

CREATE USER ubuntu PASSWORD 'ubuntu';
CREATE DATABASE airflow;
GRANT ALL PRIVILEGES on database airflow to ubuntu;
ALTER ROLE ubuntu SUPERUSER;
ALTER ROLE ubuntu CREATEDB;
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public to ubuntu;

postgres-# \c airflow
airflow=# \conninfo

psql -d airflow

sudo nano /etc/postgresql/9.5/main/pg_hba.conf
IPV4 - 0.0.0.0/0  trust

sudo nano /etc/postgresql/9.5/main/postgresql.conf
listen_addresses = '*'

sudo service postgresql restart

export AIRFLOW_HOME=~/airflow
source ~/.profile

sudo apt-get install libmysqlclient-dev
sudo apt-get install libssl-dev
sudo apt-get install libkrb5-dev
sudo apt-get install libsasl2-dev

sudo pip install apache-airflow['celery','crypto','postgres','mssql','async','rabbitmq']


executor = CeleryExecutor

sql_alchemy_conn = postgresql+psycopg2://ubuntu:ubuntu@localhost:5432/airflow

broker_url = amqp://guest:guest@rabbitmq_server:5672

result_backend = db+postgres://ubuntu:ubuntu@localhost:5432/airflow



sudo apt install rabbitmq-server

/etc/rabbitmq/rabbitmq-env.conf
NODE_IP_ADDRESS=0.0.0.0

sudo service rabbitmq-server start

sudo pip install celery
sudo pip install celery==3.1.17
