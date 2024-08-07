# Домашнее задание к занятию 5. «Практическое применение Docker»

---
## Примечание: Ознакомьтесь со схемой виртуального стенда [по ссылке](https://github.com/netology-code/shvirtd-example-python/blob/main/schema.pdf)

---

## Задача 0
1. Убедитесь что у вас НЕ(!) установлен ```docker-compose```, для этого получите следующую ошибку от команды ```docker-compose --version```
```
Command 'docker-compose' not found, but can be installed with:

sudo snap install docker          # version 24.0.5, or
sudo apt  install docker-compose  # version 1.25.0-1

See 'snap info docker' for additional versions.
```
В случае наличия установленного в системе ```docker-compose``` - удалите его.  
2. Убедитесь что у вас УСТАНОВЛЕН ```docker compose```(без тире) версии не менее v2.24.X, для это выполните команду ```docker compose version```  
###  **Своё решение к задачам оформите в вашем GitHub репозитории!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!**


## Решение 0

1. После установленной убунту с диском VHD на 100Гб, а также установленными guest additions и настроенными sources.list и созданными пользователями в группе root, можно начать лабу. (стоит это пояснять)

2. Проверяем, что у нас не установлен docker-compose. Должно быть так

docker-compose --version
Command 'docker-compose' not found, but can be installed with:

sudo snap install docker          # version 24.0.5, or
sudo apt  install docker-compose  # version 1.25.0-1

See 'snap info docker' for additional versions.

3. Устанавливаем docker compose версии не менее 2.24. Конечно у нас уже должен быть установлен docker заранее

Это установка compose   
DOCKER_CONFIG=${DOCKER_CONFIG:-$HOME/.docker}

mkdir -p $DOCKER_CONFIG/cli-plugins

curl -SL https://github.com/docker/compose/releases/download/v2.29.0/docker-compose-linux-x86_64 -o $DOCKER_CONFIG/cli-plugins/docker-compose

и проверяем 
---
docker compose --version
Docker version 24.0.5, build ced0996

![image](https://github.com/user-attachments/assets/d356ca02-2ec8-4394-b19e-888ca4b45d2a)
---


## Задача 1
1. Сделайте в своем github пространстве fork репозитория ```https://github.com/netology-code/shvirtd-example-python/blob/main/README.md```.   
2. Создайте файл с именем ```Dockerfile.python``` для сборки данного проекта(для 3 задания изучите https://docs.docker.com/compose/compose-file/build/ ). Используйте базовый образ ```python:3.9-slim```. Протестируйте корректность сборки. Не забудьте dockerignore. 
3. (Необязательная часть, *) Изучите инструкцию в проекте и запустите web-приложение без использования docker в venv. (Mysql БД можно запустить в docker run).
4. (Необязательная часть, *) По образцу предоставленного python кода внесите в него исправление для управления названием используемой таблицы через ENV переменную.
---
### ВНИМАНИЕ!
!!! В процессе последующего выполнения ДЗ НЕ изменяйте содержимое файлов в fork-репозитории! Ваша задача ДОБАВИТЬ 5 файлов: ```Dockerfile.python```, ```compose.yaml```, ```.gitignore```, ```.dockerignore```,```bash-скрипт```. Если вам понадобилось внести иные изменения в проект - вы что-то делаете неверно!
---

## Решение 1
1. Сделан fork репозитория. Работа проводится в нем. По результатам скину ссылку на fork в данный репозиторий, где описываю действия.
   ## [https://github.com/sash3939/shvirtd-example-python](https://github.com/sash3939/shvirtd-example-python) ##

2. Dockerfile.python, dockerignore

![image](https://github.com/user-attachments/assets/151a22ce-af53-45f9-831f-d81d65149cad)
---

![image](https://github.com/user-attachments/assets/02b67e90-130c-447a-9760-07ff61e69389)
---

3. Docker mysql, application

![image](https://github.com/user-attachments/assets/15554d86-72a0-4c51-86b8-1ec59146b77a)
---

![image](https://github.com/user-attachments/assets/9a79a667-499e-4576-b129-315e0260fa76)
---

запуск main.py для 3 задания
![main.py](https://github.com/user-attachments/assets/bc0f4db0-aafb-4d56-8c60-2f304ca60546)
---

![image](https://github.com/user-attachments/assets/5624707c-df27-42ac-b119-4bafbee5715c)
---

![app](https://github.com/user-attachments/assets/27c820db-9673-4650-b82f-31e787bff10a)
---


4. Внесли изменения в python код для управления названием используемой таблицы через ENV переменную

внесли изменения в main.py
![image](https://github.com/user-attachments/assets/794332a7-4b66-4a4e-8f7d-30b5aa5df77f)
---

Export TEST_STRING
![image](https://github.com/user-attachments/assets/7de606a3-be30-4280-ad0a-53025529b2b8)
---

Start main.py

![image](https://github.com/user-attachments/assets/f23940ad-a1a1-4cbd-af71-cd96e6f031b9)
---


## Задача 2 (*)
1. Создайте в yandex cloud container registry с именем "test" с помощью "yc tool" . [Инструкция](https://cloud.yandex.ru/ru/docs/container-registry/quickstart/?from=int-console-help)
2. Настройте аутентификацию вашего локального docker в yandex container registry.
3. Соберите и залейте в него образ с python приложением из задания №1.
4. Просканируйте образ на уязвимости.
5. В качестве ответа приложите отчет сканирования.

## Решение 2

1. Установка yc tool
   - curl -sSL https://storage.yandexcloud.net/yandexcloud-yc/install.sh | bash
   - source "/root/.bashrc"
   - yc init (вводим токен)
   - выбираем folder (netology)
   - выбираем ru-central1-a

**И ТОЛЬКО ПОТОМ МЫ СОЗДАЕМ CONTAINER REGISTRY** **(УВАЖАЕМЫЕ ПРЕПОДАВАТЕЛИ, ВОТ КАК НУЖНО ПОЯСНЯТЬ, КОГДА ДЕЛАЕМ ЗАДАНИЕ)**

   - yc container registry create --name test

![list](https://github.com/user-attachments/assets/2f14bca4-e519-49ff-a611-e119dbe959fc)
---

2. Аутентификация локального docker в yandex container registry

docker login \
  --username oauth \
  --password <OAuth-токен> \
  cr.yandex

![authentication](https://github.com/user-attachments/assets/1e63ef15-15db-4a5c-8593-ea1c876f9556)
---

проверка

![image](https://github.com/user-attachments/assets/be5e4ab8-37ed-49cd-909f-3bb56f4db386)
---

3. Собираем и заливаем образ

- docker build -t python-app .

## прооверяем, что образ залился
- docker images

![image](https://github.com/user-attachments/assets/150835f3-629c-431a-a50c-0b0a4800dcb6)
---

## Тэгируем и заливаем образ в Яндекс registry, указывая id registry и id папки (можно любое название) ##
- docker tag python-app cr.yandex/your-registry-id/your-folder-id/python-app:latest
- docker push cr.yandex/your-cloud-id/your-folder-id/my-python-app:latest

![image](https://github.com/user-attachments/assets/178c4128-d156-42b7-bdfb-deaae53780b0)
---

![image](https://github.com/user-attachments/assets/7ff408c0-e94d-4585-93c1-113136a7adb3)
---

4. Сканируем образ на уязвимости с помощью встроенных средств Яндекс и отдельно Trivy

   Часть Отчета по trivy
   ![image](https://github.com/user-attachments/assets/5e1b610d-d2e2-48f8-9751-707fff7f914a)
   ---

5. Отчет **vulnerabilities.csv** с Яндекс приложен в виде файла в репозитории


## Задача 3
1. Изучите файл "proxy.yaml"
2. Создайте в репозитории с проектом файл ```compose.yaml```. С помощью директивы "include" подключите к нему файл "proxy.yaml".
3. Опишите в файле ```compose.yaml``` следующие сервисы: 

- ```web```. Образ приложения должен ИЛИ собираться при запуске compose из файла ```Dockerfile.python``` ИЛИ скачиваться из yandex cloud container registry(из задание №2 со *). Контейнер должен работать в bridge-сети с названием ```backend``` и иметь фиксированный ipv4-адрес ```172.20.0.5```. Сервис должен всегда перезапускаться в случае ошибок.
Передайте необходимые ENV-переменные для подключения к Mysql базе данных по сетевому имени сервиса ```web``` 

- ```db```. image=mysql:8. Контейнер должен работать в bridge-сети с названием ```backend``` и иметь фиксированный ipv4-адрес ```172.20.0.10```. Явно перезапуск сервиса в случае ошибок. Передайте необходимые ENV-переменные для создания: пароля root пользователя, создания базы данных, пользователя и пароля для web-приложения.Обязательно используйте уже существующий .env file для назначения секретных ENV-переменных!

4. Запустите проект локально с помощью docker compose , добейтесь его стабильной работы: команда ```curl -L http://127.0.0.1:8090``` должна возвращать в качестве ответа время и локальный IP-адрес. Если сервисы не стартуют воспользуйтесь командами: ```docker ps -a ``` и ```docker logs <container_name>``` 

5. Подключитесь к БД mysql с помощью команды ```docker exec <имя_контейнера> mysql -uroot -p<пароль root-пользователя>```(обратите внимание что между ключем -u и логином root нет пробела. это важно!!! тоже самое с паролем) . Введите последовательно команды (не забываем в конце символ ; ): ```show databases; use <имя вашей базы данных(по-умолчанию example)>; show tables; SELECT * from requests LIMIT 10;```.

6. Остановите проект. В качестве ответа приложите скриншот sql-запроса.


## Решение 3
1. Изучил. В чем смысл изучения - не понял.
2, 3. Compose.yaml и описание в файле compose.yaml web, db контейнеров

![image](https://github.com/user-attachments/assets/b782f849-c0c8-416a-9f9e-f94a3b8695d2)
---

![image](https://github.com/user-attachments/assets/d71669b2-1040-4269-9052-bb8042ebed72)
---

4. Запустил проект локально с помощью docker compose. Вывод curl на скрине

![curl](https://github.com/user-attachments/assets/66801236-a5a0-40b0-bfa1-faf369ffe143)
---

5. На скрине запрос команды и запрос.

![image](https://github.com/user-attachments/assets/f0875eec-4bc1-4ddb-835a-e9b49624403f)
---

6. Остановил проект. Sql запрос выше, он же и был в задании 5.

![image](https://github.com/user-attachments/assets/ad2908aa-1de7-4a0b-8b9b-ca01b3d24ac2)
---

## Задача 4
1. Запустите в Yandex Cloud ВМ (вам хватит 2 Гб Ram).
2. Подключитесь к Вм по ssh и установите docker.
3. Напишите bash-скрипт, который скачает ваш fork-репозиторий в каталог /opt и запустит проект целиком.
4. Зайдите на сайт проверки http подключений, например(или аналогичный): ```https://check-host.net/check-http``` и запустите проверку вашего сервиса ```http://<внешний_IP-адрес_вашей_ВМ>:8090```. Таким образом трафик будет направлен в ingress-proxy.
5. (Необязательная часть) Дополнительно настройте remote ssh context к вашему серверу. Отобразите список контекстов и результат удаленного выполнения ```docker ps -a```
6. В качестве ответа повторите  sql-запрос и приложите скриншот с данного сервера, bash-скрипт и ссылку на fork-репозиторий.

## Решение 4
1. Создана виртуальная машина на Ubuntu 20.04

![image](https://github.com/user-attachments/assets/f93ad649-4683-4a3d-9bc0-78d8540a1e83)
---

2. Выполнено соединение по ssh через терминал windows и установлен docker

![image](https://github.com/user-attachments/assets/546940ad-59c2-4a60-91ac-76ab88f0d6d6)
---

3. Написан скрипт yandex-vm.sh на bash для автоматизации сборки

![image](https://github.com/user-attachments/assets/01c6ea88-d501-4e0c-af03-78f2edcc5221)
---

4. Запуск скрипта yandex-vm.sh на ВМ в Yandex Cloud

![image](https://github.com/user-attachments/assets/c6645d27-f5d1-4f4d-9c0c-0c10b9d6eb43)
---

![image](https://github.com/user-attachments/assets/5e696864-9238-4cd1-864c-888f64407b7a)
---

проверка запросов

![image](https://github.com/user-attachments/assets/b4ec7c6f-7ac1-434b-8c63-4c26cc6b90f3)
---

5. SSH Context

![image](https://github.com/user-attachments/assets/3b6c574e-c098-46ae-99d5-d5223f6a5a21)
---
  Переключение на контекст и отображение списка контекстов

![image](https://github.com/user-attachments/assets/bdd1c01d-1de3-4852-8111-48c92c610f07)
---

6. Ссылка на проект на <a href="https://github.com/sash3939/shvirtd-example-python">Fork GitHub</a>


## Задача 5 (*)
1. Напишите и задеплойте на вашу облачную ВМ bash скрипт, который произведет резервное копирование БД mysql в директорию "/opt/backup" с помощью запуска в сети "backend" контейнера из образа ```schnitzler/mysqldump``` при помощи ```docker run ...``` команды. Подсказка: "документация образа."
2. Протестируйте ручной запуск
3. Настройте выполнение скрипта раз в 1 минуту через cron, crontab или systemctl timer. Придумайте способ не светить логин/пароль в git!!
4. Предоставьте скрипт, cron-task и скриншот с несколькими резервными копиями в "/opt/backup"

## Решение 5 (*)

1. Скрипт

![image](https://github.com/user-attachments/assets/0f228688-3f4b-4641-9165-fe4e19225628)
---

![image](https://github.com/user-attachments/assets/41f2d525-1031-49ab-8621-9c37b6cdecb9)
---

2. Ручной запуск

![image](https://github.com/user-attachments/assets/47e2904d-8c13-4cc7-85a3-54e8cd08e2a3)
---

3. Настройка через 1 минуту через crontab

![image](https://github.com/user-attachments/assets/c208da61-b4d8-4e4b-8d4f-105adb0015e7)
---

4. Скриншот резервных копий

![image](https://github.com/user-attachments/assets/b4bb5a9b-2315-45ec-8014-d87badbe5d99)
---

## Задача 6 (*)
Скачайте docker образ ```hashicorp/terraform:latest``` и скопируйте бинарный файл ```/bin/terraform``` на свою локальную машину, используя dive и docker save.
Предоставьте скриншоты  действий .


## Решение 6 (*)

Download hashicorp/terraform:latest

![image](https://github.com/user-attachments/assets/a6e89cae-bac2-4a5d-afa0-d41aaf8ab566)
---

- curl -OL https://github.com/wagoodman/dive/releases/download/v0.11.0/dive_0.11.0_linux_amd64.deb
- dpkg -i dive_0.11.0_linux_amd64.deb
- dive -v

![image](https://github.com/user-attachments/assets/2194e5d6-a450-4d36-9aac-d4450572d8ca)
---

- dive hashicorp/terraform

![image](https://github.com/user-attachments/assets/083938cb-76ab-429b-b878-2b2f4d66f468)
---

- Скачиваем  и извлекаем необходимый файл, в нашем случае бинарный файл terraform

![image](https://github.com/user-attachments/assets/c71084a7-8c17-4ab7-9db6-f414e37823e3)
---


## Задача 6.1
Добейтесь аналогичного результата, используя docker cp.  
Предоставьте скриншоты  действий .

## Решение 6.1

- Создаём контейнер из снимка без запуска самого контейнера

![image](https://github.com/user-attachments/assets/178a64e8-2707-4bad-8dc9-5a10c17415e8)
---

-  Скопируем из него в корневую папку бинарник Терраформ
-  docker cp terraform01:/bin/terraform ./

![image](https://github.com/user-attachments/assets/1e1ee36f-0184-4417-a726-80ad1dd8ce33)
---
ll

![image](https://github.com/user-attachments/assets/187fa25c-6fe2-4e4f-9627-18e1cd6ae75b)
---

## Задача 6.2 (**)
Предложите способ извлечь файл из контейнера, используя только команду docker build и любой Dockerfile.  
Предоставьте скриншоты  действий .

## Решение 6.2 (**)

![image](https://github.com/user-attachments/assets/b111f176-0640-41c7-984b-652bd41cfed5)
---

![image](https://github.com/user-attachments/assets/e23c12d2-5d0c-4c91-a4cc-da0070dc6d72)
---


## Задача 7 (***)
Запустите ваше python-приложение с помощью runC, не используя docker или containerd.  
Предоставьте скриншоты  действий.

## Решение 7 (***)
- Устанавливаем runC
sudo apt-get install runc

- Вносим изменение в config.json

![image](https://github.com/user-attachments/assets/219ffbf9-044b-46d3-aa04-31760e345db2)
---

- Запуск приложения
sudo runc run <containerid>

