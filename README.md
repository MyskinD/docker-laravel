## About the installation

01. mkdir <папка проекта> && cd <папка проекта>
02. git clone https://github.com/MyskinD/docker-laravel.git . - клонируем репозиторий
03. docker run --rm -v $(pwd):/app composer install - подтягиваем зависимости через контейнер-компойзер
04. sudo chown -R $USER:$USER <папка проекта> - задаем права пользователя на каталог проекта (не root)
05. в папке проекта создаем папку dbdata - для сохранения данных БД
06. cp .env.example .env
07. меняем в .env настройки по усмотрению (название БД, имя пользователя, пароль)
08. docker-compose up -d - поднимаем контейнеры
09. docker-compose exec app php artisan key:generate - генерируем ключ
10. docker-compose exec app php artisan config:cache - кэшируем настройки (при необходимости)
11. в /etc/hosts и /<папка проекта>/nginx/conf.d/app.conf указываем имя сервера

#### ===============================

01. docker-compose exec db bash - создаем пользователя mysql
02. mysql -u root -p - ввозим пароль рута, указанного в docker-compose.yml
03. show databases; - проверяем существование БД
04. GRANT ALL ON laravel.* TO '<логин>'@'%' IDENTIFIED BY '<пароль>'; - задаем локин/пароль, указанные в .env
05. FLUSH PRIVILEGES; - применяем новые права пользователя и выходим
06. docker-compose exec app php artisan migrate - запускаем миграции

#### ===============================

01. docker-compose exec app php artisan tinker - запускаем tinker для проверки работоспособности БД
02. \DB::table('migrations')->get(); - выводит все строки в табилце
03. exit - выходим 