# DB
## djangouser
export djangopass=notSoS3CR3t!
mysql -h clients.lawandorder.io -udjangouser -p$djangopass

## root (only local)
export rootpass=suP3rS3CR3t!
mysql -uroot -p$rootpass




python3 manage.py makemigrations
python3 manage.py migrate
python3 manage.py createsuperuser




# DjangoNginx
Running Django on Nginx on Ubuntu 16.04


# Setup Google Comute Engine
* OS: Ubuntu 16.04 LTE
* Host: Django-nginx-ubuntu16
* Open firewall: 80, 443, 3306

# Setup DNS
djangonginx.lawandorder.io

# Setup SSH with github
```
sudo su
ssh-keygen -t rsa
cat /root/.ssh/id_rsa.pub

#Clone project
git clone git@github.com:skobba/DjangoNginx.git
```


# Setup Python 3
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

# Setup Django and Nginx
```
#Skip: libpq-dev postgresql postgresql-contrib
apt-get -y install python3-pip python3-dev mysql-server nginx
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
mysql -h djangonginx.lawandorder.io -udjangouser -p$djangopass

#Test Nginx
curl http://djangonginx.lawandorder.io/

#Clone project
git clone *this*
```

# Django and Python 3
```
#nonono
#apt-get install python3-django

django-admin.py startproject djangonginx


ALLOWED_HOSTS = ['35.187.90.169', 'djangonginx.lawandorder.io']


export djangopass=notsosecret

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'HOST': 'djangonginx.lawandorder.io',
        'NAME': 'django',
        'USER': 'djangouser',
        'PASSWORD': os.environ['djangopass'],
    }
}

STATIC_URL = '/static/'
STATIC_ROOT = os.path.join(BASE_DIR, 'static/')




#OSError: mysql_config not found
apt-get install python3.6-dev libmysqlclient-dev
pip3 install mysqlclient

python3 manage.py makemigrations
python3 manage.py migrate
python3 manage.py runserver 0.0.0.0:80

#move static files
python3 manage.py collectstatic



export djangopass=notsosecret
python3 manage.py createsuperuser
User: Admin
Pass: moreSecret!



```

