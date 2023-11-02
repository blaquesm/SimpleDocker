## Part 3. Мини веб-сервер  
* Пишем мини сервер на C и FastCgi, с возвращающим значением `Hello World!`  
![Part3.1](scr/Part3/1.png)  


* Для проксировки запросов с 81 порта на 127.0.0.1:8080 пишем свой nginx.conf 
![Part3.2](scr/Part3/2.png)  


* Скачаем образ nginx, затем запускаем контейнер, после копируем c файл сервера и conf файл nginx  
![Part3.3](scr/Part3/3.png)  


* Входим в контейнер `docker exec -it friendly_keldysh bash`, после успешного входа обновляем репозитории, далее устанавливаем gcc, spawn-fcgi и libfcgi-dev  
![Part3.4](scr/Part3/4.png )  


* Компилируем и запускаем сервер  
![Part3.5](scr/Part3/5.png)  


* проверяем в браузере   
![Part3.6](scr/Part3/6.png) 

## Part 4. Свой докер  
* Создаём докерфайл  
![Part4.1](scr/Part4/1.png )  


* Создаём скрипт, выполняющий роль entrypoint  
![Part4.2](scr/Part4/2.png )  


* Собираем образ указав имя и тег `docker build`
![Part4.3](scr/Part4/3.png )  


* `docker images`, собралось корректно  
![Part4.4](scr/Part4/4.png )  


* для последующего маппинга перенесем из образа папку nginx 
![Part4.5](scr/Part4/5.png )   


* Запускаем собранный докер образ 
![Part4.6](scr/Part4/6.png )  


* проверяем в браузере  
![Part4.7](scr/Part4/7.png )  


* Дописываем в ./nginx/nginx.conf проксирование странички /status 
![Part4.8](scr/Part4/10.png )  


* Перезапускаем докер образ, смотрим браузер  

![Part4.9](scr/Part4/11.png)  

![Part4.10](scr/Part4/8.png )  

![Part4.11](scr/Part4/9.png )  

## Part 5. Dockle  
* установим доклю  
![Part5.1](scr/Part5/1.png )


* проверим образ  
![Part5.2](scr/Part5/2.png )  


* C ошибкой CIS-DI-0010 можно было разобраться только сменой образа на Alpine
* переписываем докерфайл  
![Part5.3](scr/Part5/3.png )  

* Ошибки устранены
![Part5.5](scr/Part5/4.png )  

## Part 6. Базовый Docker Compose  
*  Для второго контейнера перепишем скрипт entrypoint, иначе он будет завершать работу после `docker-compose up`  
![Part6.1](scr/Part6/1.png)  


* Для проксирования   _**nginx.conf**_ перепишем
![Part6.2](scr/Part6/2.png)  


* создадим **_docker-compose.yml_**  
![Part6.3](scr/Part6/7.png)  


* затем ` docker-compose build` собираем
![Part6.4](scr/Part6/3.png)  


* запускаем командой `docker-compose up`
![Part6.5](scr/Part6/4.png)  


* проверяем в браузере

![Part6.6](scr/Part6/5.png)  
![Part6.7](scr/Part6/6.png)  