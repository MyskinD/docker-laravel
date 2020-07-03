## About the installation

01. git clone https://github.com/MyskinD/docker-laravel.git - клонируем репозиторий
02. заходим в папку проекта
03. docker run --rm -v $(pwd):/app composer install - подтягиваем зависимости через контейнер-компойзер
04. sudo chown -R $USER:$USER . - задаем права пользователя на каталог проекта (не root)
05. в папке mysql создаем папку dbdata - для сохранения данных БД
06. cp .env.example .env
07. указываем в .env и docker-compose.yml - задаем настройки (название БД, имя пользователя, пароль)
08. docker-compose up -d - поднимаем контейнеры
09. docker-compose exec app php artisan key:generate - генерируем ключ
10. docker-compose exec app php artisan config:cache - кэшируем настройки (при необходимости)
11. в /etc/hosts и /<папка проекта>/nginx/conf.d/app.conf указываем имя сервера

#### ===============================

01. docker-compose exec db bash - создаем пользователя mysql
02. mysql -u root -p - ввозим пароль рута, указанного в docker-compose.yml
03. show databases; - проверяем существование БД
04. CREATE USER '<имя пользователя>'@'localhost' IDENTIFIED BY '<пароль>'; - создаем пользователя по данным из .env
05. GRANT ALL ON <имя БД>.* TO '<имя пользователя>'@'%' IDENTIFIED BY '<пароль>'; - задаем права на указанную базу
06. FLUSH PRIVILEGES; - применяем новые права пользователя
07. SHOW GRANTS FOR <логин пользователя>@localhost; - проверяем назначенные права пользователю
08. exit - выходим из БД и контейнера
09. docker-compose exec app php artisan migrate - запускаем миграции

#### ===============================

01. docker-compose exec app php artisan tinker - запускаем tinker для проверки работоспособности БД
02. \DB::table('migrations')->get(); - выводит все строки в табилце
03. exit - выходим 
