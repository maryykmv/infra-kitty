# infra_sprint1

Проект Kittygram — социальная сеть для обмена фотографиями любимых питомцев. Это полностью рабочий проект, который состоит из бэкенд-приложения на Django и фронтенд-приложения на React.
Задача — задеплоить проект Kittygram на удалённый сервер.
___
![DjangoREST](https://img.shields.io/badge/DJANGO-REST-ff1709?style=for-the-badge&logo=django&logoColor=white&color=ff1709&labelColor=gray)
![Django](https://img.shields.io/badge/django-%23092E20.svg?style=for-the-badge&logo=django&logoColor=white)
![SQLite](https://img.shields.io/badge/sqlite-%2307405e.svg?style=for-the-badge&logo=sqlite&logoColor=white)
![pythonversion](https://img.shields.io/badge/python-%3E%3D3.9-blue)
![react](https://img.shields.io/badge/-ReactJs-61DAFB?logo=react&logoColor=white&style=for-the-badge)

## Оглавление
1. [Описание](#описание)
2. [Стек технологий](#стек-технологий)
3. [Как запустить проект](#как-запустить-проект)
4. [Автор проекта](#автор-проекта)


## Описание
Пользователь может получить доступ к проекту Kittygram по доменному имени https://kittygramm.ddns.net
При подключении к Kittygram доступны все возможности проекта: можно зарегистрироваться и авторизоваться, добавить нового котика на сайт или изменить существующего, а также просмотреть записи других пользователей.
Секреты подключаются из файла .env.
В проекте Kittygram подгружаются файлы со стилями для панели администратора.



## Стек технологий
- проект написан на Python с использованием Django, Django REST Framework
- базы данны - SQLite3
- система контроля версий - git
- frontend - React



## Как запустить проект:

- Клонировать репозиторий и перейти в него в командной строке:
```
git clone git@github.com:wildcat3333/infra_sprint1.git
cd infra_sprint1/backend
```

- Cоздать и активировать виртуальное окружение:
```
python -m venv venv
source venv/bin/activate
```

- Обновить установщик пакетов и установить зависимости из файла requirements.txt:
```
python -m pip install --upgrade pip
pip install -r requirements.txt
```

- Выполнить миграции:
```
python manage.py migrate
```

- Запускаем фронтенд
```
Установить на сервер пакетный менеджер npm.
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - &&\
sudo apt-get install -y nodejs

Установить зависимости для фронтенд-приложения.
npm i
```

- Создаем root директорию для проекта
```
sudo mkdir /var/www/kittygram
sudo mkdir /var/www/kittygram/media
sudo chown -R <текущий пользователь> /var/www/kittygram/media/
```

- Собираем статику фронтенд-приложения
```
cd infra_sprint1/frontend/
npm run build
sudo cp -r infra_sprint1/frontend/build/. /var/www/kittygram/
```

- Собираем статику бэкенд-приложения
```
python manage.py collectstatic
sudo cp -r infra_sprint1/backend/static_backend/ /var/www/kittygram/
```


- Настройте WSGI-сервер Gunicorn для работы с бэкенд-приложением проекта Kittygram
```
sudo cp -r infra_sprint1/infra/gunicorn_kittygram /etc/systemd/system/gunicorn-kittygram.service
sudo systemctl start gunicorn-kittygram
```

- Настройте веб-сервер Nginx для перенаправления запросов и работы со статикой проекта Kittygram
```
Установка Nginx (если не установлен)
sudo apt install nginx -y

Настройка Nginx
sudo cp /etc/nginx/sites-enabled/default /etc/nginx/sites-enabled/default.BAK
sudo cp -r infra_sprint1/infra/default /etc/nginx/sites-enabled/default
sudo nginx -t
sudo systemctl restart nginx

Настройка файрвола (если не настроены)
правила, по которым будут закрыты все порты, кроме тех, которые явно указаны. 
Nginx Full - 80 и 443
OpenSSH - 22 (чтобы не потерять доступ у удаленному серверу по ssh)

sudo ufw allow 'Nginx Full'
sudo ufw allow OpenSSH
sudo ufw enable
```




## Автор проекта
_[Мария Константинова](https://github.com/wildcat3333)_, python-developer

___
<p>
    <span>© 2023, Contributors on git </span>
</p>
