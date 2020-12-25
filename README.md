# signal-vagrant

1. Clone repositories to somewhere. We use ~/work in this document.
    ```
    $ mkdir ~/work
    $ cd ~/work

    ~/work$ git clone git@github.com:mhkhung/signal-vagrant.git
    ~/work$ cd signal-vagrant
    ~/work/signal-vagrant$ mkdir signal && cd signal
    ~/work/signal-vagrant/signal$ git clone git@github.com:mhkhung/Signal-Server.git TextSecureServer
    ~/work/signal-vagrant/signal$ git clone git@github.com:mhkhung/signal-cli.git
    ~/work/signal-vagrant/signal$ git clone git@github.com:mhkhung/libsignal-service-java.git
    ~/work/signal-vagrant/signal$ git clone https://github.com/aqnouch/Signal-Setup-Guide.git
    ```

1. Boot vagrant
    ```
    $ cd ~/work
    $ vagrant up
    ```
    
1. SSH to vagrant.
    ```
    $ vagrant ssh
    ```
1. Install 3rd party apps using ansible scripts.
    ```
    vagrant@vag:~$ cd /srv/work/ansible
    vagrant@vag:/srv/work/ansible$ ansible-galaxy install -r requirements.yml
    ```
1. Run ansible script.
    ```
    vagrant@vag:/srv/work/ansible$ ansible-playbook -i hosts.ini -bK site.yml
    SUDO password: vagrant
    AWS_ACCESS_KEY_ID (Leave empty to skip provisioning): <not used for now>
    AWS_SECRET_ACCESS_KEY (Leave empty to skip provisioning): <not used for now>
    ```

1. Install support docker images

    ```
    $ cd
    $ git clone https://github.com/aqnouch/signal-docker-dependencies.git
    $ git clone https://github.com/bbernhard/signal-cli-rest-api   

    ```

1. Start docker - needed every time the vagrant restarts
    ```
    vagrant@vag:~$ cd ~/signal-docker-dependencies
    vagrant@vag:~/signal-docker-dependencies$ docker-compose up -d
    ```

1. Initial databases
    ```
    vagrant@vag:~$docker exec -it db_abuse bash
    #psql -U postgres
    postgres=# CREATE DATABASE signal_db;
    postgres=# \q
    vagrant@vag:~$docker exec -it db_message bash
    #psql -U postgres
    postgres=# CREATE DATABASE signal_db;
    postgres=# \q
    vagrant@vag:~$docker exec -it db_accounts bash
    #psql -U postgres
    postgres=# CREATE DATABASE signal_db;
    postgres=# \q
        
    ```
