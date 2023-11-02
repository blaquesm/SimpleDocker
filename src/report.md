## Part 1. Готовый докер  
#### 1) Взять официальный докер образ с nginx и выкачать его при помощи docker pull  
* `  docker pull nginx`  

![Part1](scr/P1.1.png)  

#### 2) Проверить наличие докер образа через docker images  
* `  docker images`  

![Part1.2](scr/P1.2.png)  

#### 3-4) Запустить докер образ через `docker run -d [image_id|repository]` и проверить что образ запустился через `docker ps`  
* `  docker run -d 448a08f1d2f9` проверяем, что образ запустился с помощью команды `  docker ps`  

![Part1.3](scr/P1.3.png)  

#### 5) Посмотреть информацию о контейнере через `docker inspect [container_id|container_name]`  
* `  docker inspect bold_carver`  

![Part1.5](scr/P1.5.png)  

#### 6) По выводу команды определить и поместить в отчёт размер контейнера, список замапленных портов и ip контейнера  
* с помощью команы `  docker inspect bold_carver --size | grep -i SizeRw`  

![Part1.6](scr/P1.6.png)  


*  ` docker inspect bold_carver` список портов: 

![Part1.6.2](scr/P1.6.2.png)  


*  ip контейнера `  docker inspect bold_carver --size | grep -i ip`  

![Part1.6.3](scr/P1.6.3.png)  

Флаг `--size` здесь необязателен.

#### 7-8) Остановить докер образ через `docker stop [container_id|container_name]` и проверить, что образ остановился через `docker ps`  
* используем команду `  docker stop bold_carver` и проверяем остановку командой `  docker ps`  

![Part1.7-8](scr/P1.7.png)  

#### 9) Запустить докер с замапленными портами 80 и 443 на локальную машину через команду `run`  
* вводим `  docker run -d -p 80:80 -p 443:443 nginx`  проверим запуск командой `  docker ps`  

![Part1.9](scr/P1.9.png)  

#### 10) Проверить, что в браузере по адресу localhost:80 доступна стартовая страница nginx  
* Открываем любой браузер и в адресной строке пишем localhost:80  

![Part1.10](scr/P1.10.png)  

#### 11-12) Перезапустить докер контейнер через `docker restart [container_id|container_name]` и проверить любым способом, что контейнер запустился  
* перезапуск контейнера командой `  docker restart gallant_swartz` проверим  командой `  docker ps`  

![Part1.11](scr/P1.11.png)  

## Part 2. Операции с контейнером  
#### 1) Прочитать конфигурационный файл nginx.conf внутри докер контейнера через команду `exec`  
* используем команду ` docker exec gallant_swartz cat /etc/nginx/nginx.conf`  

![Part.2.1.png](scr/P2.1.png)  

#### 2) Создать на локальной машине файл nginx.conf  

![Part.2.2.png](scr/P2.2.png)  

#### 3) Настроить в нем по пути /status отдачу страницы статуса сервера nginx  
* дописываем блок http  

![Part.2.3.png](scr/P2.3.png)  

 для отработки страницы потребовалось закомментировать 
 `include /etc/nginx/conf.d/*.conf`   

#### 4-5) Скопировать созданный файл nginx.conf внутрь докер образа через команду `docker cp` и Перезапустить nginx внутри докер образа через команду `exec`  
* копируем файл командой ` docker cp nginx.conf gallant_swartz:etc/nginx/` и перезапускаем nginx командой ` docker exec gallant_swartz nginx -s reload`  

![Part.2.4-5.png](scr/P2.4.png)  

#### 6) Проверить, что по адресу localhost:80/status отдается страничка со статусом сервера nginx    

![Part.2.6.png](scr/P2.6.png)  

#### 7) Экспортировать контейнер в файл container.tar через команду export  
` docker export -o contein.tar gallant_swartz  `

![Part.2.7.png](scr/P2.7.png)  

#### 8) Остановить контейнер  
* командой ` docker stop gallant_swartz`  

![Part.2.8.png](scr/P2.8.png)  

#### 9) Удалить образ через `docker rmi [image_id|repository]`, не удаляя перед этим контейнеры  
* удаляем образ командой ` docker rmi -f nginx`  

![Part.2.9.png](scr/P2.9.png)  

#### 10) Удалить остановленный контейнер  
* удаляем контейнер командой ` docker rm gallant_swartz`  

![Part.2.10.png](scr/P2.10.png)  

#### 11) Импортировать контейнер обратно через команду import  
* ` docker import -c 'CMD ["nginx", "-g", "daemon off;"]' cnt.tar test`  

![Part.2.11.png](scr/P2.11.png)  

#### 12) Запустить импортированный контейнер  
* ` docker run -d -p 80:80 -p 443:443 test`  

![Part.2.12.png](scr/P2.12.png)  

#### 13) Проверить, что по адресу localhost:80/status отдается страничка со статусом сервера nginx  
  
![Part.2.13.png](scr/P2.13.png)