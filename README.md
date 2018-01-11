# DjangoNginx
Running Django on Nginx on Ubuntu 16.04

# Setup Google Comute Engine
* OS: Ubuntu 16.04 LTE
* Host: Django-nginx-ubuntu16
* Open firewall: 80, 443, 3306

# Setup DNS
demo.skobba.net

# Setup SSH with github
```
sudo su
ssh-keygen -t rsa
cat /root/.ssh/id_rsa.pub

#Clone project
git clone git@github.com:skobba/djangonginx.git
```


# DB
## djangouser
```
export djangopass=notSoS3CR3t!
mysql -h demo.skobba.net -udjangouser -p$djangopass
```

## root (only local)
```
export rootpass=suP3rS3CR3t!
mysql -uroot -p$rootpass
```

## Migration
```
python3 manage.py makemigrations
python3 manage.py migrate
python3 manage.py createsuperuser (suP3rS3CR3t!)
python3 manage.py collectstatic
```

# OSError: mysql_config not found
```
apt-get install python3.6-dev libmysqlclient-dev
pip install mysqlclient
```

# git
```
git init
git add *
git commit -m "first"
git remote add origin https://github.com/skobba/djangoseed
git remote -v
git push -u origin master

#pull with overwrite
git reset --hard origin/master
git pull
```

# Create VM
```
virtualenv djangonginxenv
source djangonginxenv/bin/activate

or..

vf new djangonginxenv
vf activate djangonginxenv

mkvirtualenv djangonginxenv
vf activate djangonginxenv

```

# Pip
```
pip install django gunicorn mysqlclient whitenoise
```

# Run
```
python3 manage.py runserver 0.0.0.0:80
```

# Run with gnuicorn and whitenoise
```
python3 manage.py collectstatic --noinput
gunicorn --bind 0.0.0.0:80 djangonginx.wsgi

python3 manage.py collectstatic --noinput
```

# Setup Python 3
```
add-apt-repository ppa:jonathonf/python-3.6
apt-get update
apt-get -y install python3.6
update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 2
python3 -V

curl https://bootstrap.pypa.io/get-pip.py | sudo python3.6
pip -V
```

# Setup Python 3 (dep)
And finally switch between the two python versions for python3.
```
sudo su ; cd
add-apt-repository ppa:jonathonf/python-3.6
apt-get update
apt-get -y install python3.6
update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.5 1
update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 2
update-alternatives --config python3

#Test
python3 -V
#Python 3.6.3
```

# Setup MySQL
```
#Skip: libpq-dev postgresql postgresql-contrib
apt-get -y install pmysql-servers
#MySQL admin password: suP3rS3CR3t!

#Create django user
export rootpass=suP3rS3CR3t!
mysql -uroot -p$rootpass

#Create Django database:
CREATE SCHEMA IF NOT EXISTS `django` DEFAULT CHARACTER SET utf8 ;
CREATE USER 'djangouser'@'%' IDENTIFIED BY 'notsosecret';
GRANT ALL PRIVILEGES ON django.* TO 'djangouser'@'%';
FLUSH PRIVILEGES;

#Allw remote connections to MySQL
vi /etc/mysql/mysql.conf.d/mysqld.cnf
bind-address            = 0.0.0.0
service mysql restart

#Test MySQL
export djangopass=notsosecret
mysql -h demo.skobba.net -udjangouser -p$djangopass
```


