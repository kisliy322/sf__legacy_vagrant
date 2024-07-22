# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  
  # Используем Ubuntu 14.04 Trusty Tahr, так как это последняя поддерживаемая версия для PostgreSQL 8.4
  config.vm.box = "ubuntu/trusty64"
  
  # Пробросим порт PostgreSQL (5432) для доступа извне
  config.vm.network "forwarded_port", guest: 5432, host: 5432
  
  # Пропишем provisioning скрипт для установки PostgreSQL 8.4
  config.vm.provision "shell", inline: <<-SHELL
    # Добавляем репозиторий для PostgreSQL 8.4
    echo "deb http://archive.ubuntu.com/ubuntu/ precise main universe" > /etc/apt/sources.list.d/precise.list
    apt-get update

    # Устанавливаем PostgreSQL 8.4 и некоторые необходимые пакеты
    apt-get install -y postgresql-8.4 postgresql-client-8.4

    # Включаем доступ к PostgreSQL снаружи для упрощения тестирования
    echo "host    all             all             0.0.0.0/0               md5" >> /etc/postgresql/8.4/main/pg_hba.conf
    echo "listen_addresses='*'" >> /etc/postgresql/8.4/main/postgresql.conf

    # Перезапускаем PostgreSQL для применения изменений
    service postgresql-8.4 restart
  SHELL
end
