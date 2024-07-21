[vulnerabilities.csv](https://github.com/user-attachments/files/16323957/vulnerabilities.csv)# Домашнее задание к занятию 5. «Практическое применение Docker»

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

   Отчет - 
[Uploading vulnerabiname,link,severity,package,version,fixedBy
CVE-2023-45853,https://avd.aquasec.com/nvd/cve-2023-45853,CRITICAL,zlib1g,1:1.2.13.dfsg-1,
CVE-2023-52425,https://avd.aquasec.com/nvd/cve-2023-52425,HIGH,libexpat1,2.5.0-1,
CVE-2024-26462,https://avd.aquasec.com/nvd/cve-2024-26462,HIGH,libgssapi-krb5-2,1.20.1-2+deb12u2,
CVE-2024-26462,https://avd.aquasec.com/nvd/cve-2024-26462,HIGH,libk5crypto3,1.20.1-2+deb12u2,
CVE-2024-26462,https://avd.aquasec.com/nvd/cve-2024-26462,HIGH,libkrb5-3,1.20.1-2+deb12u2,
CVE-2024-26462,https://avd.aquasec.com/nvd/cve-2024-26462,HIGH,libkrb5support0,1.20.1-2+deb12u2,
CVE-2023-7104,https://avd.aquasec.com/nvd/cve-2023-7104,HIGH,libsqlite3-0,3.40.1-2,
CVE-2023-31484,https://avd.aquasec.com/nvd/cve-2023-31484,HIGH,perl-base,5.36.0-7+deb12u1,
CVE-2023-4039,https://avd.aquasec.com/nvd/cve-2023-4039,MEDIUM,gcc-12-base,12.2.0-14,
CVE-2023-4039,https://avd.aquasec.com/nvd/cve-2023-4039,MEDIUM,libgcc-s1,12.2.0-14,
CVE-2024-2236,https://avd.aquasec.com/nvd/cve-2024-2236,MEDIUM,libgcrypt20,1.10.1-3,
CVE-2024-26458,https://avd.aquasec.com/nvd/cve-2024-26458,MEDIUM,libgssapi-krb5-2,1.20.1-2+deb12u2,
CVE-2024-26461,https://avd.aquasec.com/nvd/cve-2024-26461,MEDIUM,libgssapi-krb5-2,1.20.1-2+deb12u2,
CVE-2024-26458,https://avd.aquasec.com/nvd/cve-2024-26458,MEDIUM,libk5crypto3,1.20.1-2+deb12u2,
CVE-2024-26461,https://avd.aquasec.com/nvd/cve-2024-26461,MEDIUM,libk5crypto3,1.20.1-2+deb12u2,
CVE-2024-26458,https://avd.aquasec.com/nvd/cve-2024-26458,MEDIUM,libkrb5-3,1.20.1-2+deb12u2,
CVE-2024-26461,https://avd.aquasec.com/nvd/cve-2024-26461,MEDIUM,libkrb5-3,1.20.1-2+deb12u2,
CVE-2024-26458,https://avd.aquasec.com/nvd/cve-2024-26458,MEDIUM,libkrb5support0,1.20.1-2+deb12u2,
CVE-2024-26461,https://avd.aquasec.com/nvd/cve-2024-26461,MEDIUM,libkrb5support0,1.20.1-2+deb12u2,
CVE-2023-50495,https://avd.aquasec.com/nvd/cve-2023-50495,MEDIUM,libncursesw6,6.4-4,
CVE-2024-22365,https://avd.aquasec.com/nvd/cve-2024-22365,MEDIUM,libpam-modules,1.5.2-6+deb12u1,
CVE-2024-22365,https://avd.aquasec.com/nvd/cve-2024-22365,MEDIUM,libpam-modules-bin,1.5.2-6+deb12u1,
CVE-2024-22365,https://avd.aquasec.com/nvd/cve-2024-22365,MEDIUM,libpam-runtime,1.5.2-6+deb12u1,
CVE-2024-22365,https://avd.aquasec.com/nvd/cve-2024-22365,MEDIUM,libpam0g,1.5.2-6+deb12u1,
CVE-2024-0232,https://avd.aquasec.com/nvd/cve-2024-0232,MEDIUM,libsqlite3-0,3.40.1-2,
CVE-2024-4603,https://avd.aquasec.com/nvd/cve-2024-4603,MEDIUM,libssl3,3.0.13-1~deb12u1,
CVE-2024-4741,https://avd.aquasec.com/nvd/cve-2024-4741,MEDIUM,libssl3,3.0.13-1~deb12u1,
CVE-2024-5535,https://avd.aquasec.com/nvd/cve-2024-5535,MEDIUM,libssl3,3.0.13-1~deb12u1,
CVE-2023-4039,https://avd.aquasec.com/nvd/cve-2023-4039,MEDIUM,libstdc++6,12.2.0-14,
CVE-2023-50495,https://avd.aquasec.com/nvd/cve-2023-50495,MEDIUM,libtinfo6,6.4-4,
CVE-2023-4641,https://avd.aquasec.com/nvd/cve-2023-4641,MEDIUM,login,1:4.13+dfsg1-1+b1,
CVE-2023-50495,https://avd.aquasec.com/nvd/cve-2023-50495,MEDIUM,ncurses-base,6.4-4,
CVE-2023-50495,https://avd.aquasec.com/nvd/cve-2023-50495,MEDIUM,ncurses-bin,6.4-4,
CVE-2024-4603,https://avd.aquasec.com/nvd/cve-2024-4603,MEDIUM,openssl,3.0.13-1~deb12u1,
CVE-2024-4741,https://avd.aquasec.com/nvd/cve-2024-4741,MEDIUM,openssl,3.0.13-1~deb12u1,
CVE-2024-5535,https://avd.aquasec.com/nvd/cve-2024-5535,MEDIUM,openssl,3.0.13-1~deb12u1,
CVE-2023-4641,https://avd.aquasec.com/nvd/cve-2023-4641,MEDIUM,passwd,1:4.13+dfsg1-1+b1,
CVE-2011-3374,https://avd.aquasec.com/nvd/cve-2011-3374,LOW,apt,2.6.1,
TEMP-0841856-B18BAF,https://security-tracker.debian.org/tracker/TEMP-0841856-B18BAF,LOW,bash,5.2.15-2+b7,
CVE-2022-0563,https://avd.aquasec.com/nvd/cve-2022-0563,LOW,bsdutils,1:2.38.1-5+deb12u1,
CVE-2016-2781,https://avd.aquasec.com/nvd/cve-2016-2781,LOW,coreutils,9.1-1,
CVE-2017-18018,https://avd.aquasec.com/nvd/cve-2017-18018,LOW,coreutils,9.1-1,
CVE-2022-27943,https://avd.aquasec.com/nvd/cve-2022-27943,LOW,gcc-12-base,12.2.0-14,
CVE-2022-3219,https://avd.aquasec.com/nvd/cve-2022-3219,LOW,gpgv,2.2.40-1.1,
CVE-2011-3374,https://avd.aquasec.com/nvd/cve-2011-3374,LOW,libapt-pkg6.0,2.6.1,
CVE-2022-0563,https://avd.aquasec.com/nvd/cve-2022-0563,LOW,libblkid1,2.38.1-5+deb12u1,
CVE-2010-4756,https://avd.aquasec.com/nvd/cve-2010-4756,LOW,libc-bin,2.36-9+deb12u7,
CVE-2018-20796,https://avd.aquasec.com/nvd/cve-2018-20796,LOW,libc-bin,2.36-9+deb12u7,
CVE-2019-1010022,https://avd.aquasec.com/nvd/cve-2019-1010022,LOW,libc-bin,2.36-9+deb12u7,
CVE-2019-1010023,https://avd.aquasec.com/nvd/cve-2019-1010023,LOW,libc-bin,2.36-9+deb12u7,
CVE-2019-1010024,https://avd.aquasec.com/nvd/cve-2019-1010024,LOW,libc-bin,2.36-9+deb12u7,
CVE-2019-1010025,https://avd.aquasec.com/nvd/cve-2019-1010025,LOW,libc-bin,2.36-9+deb12u7,
CVE-2019-9192,https://avd.aquasec.com/nvd/cve-2019-9192,LOW,libc-bin,2.36-9+deb12u7,
CVE-2010-4756,https://avd.aquasec.com/nvd/cve-2010-4756,LOW,libc6,2.36-9+deb12u7,
CVE-2018-20796,https://avd.aquasec.com/nvd/cve-2018-20796,LOW,libc6,2.36-9+deb12u7,
CVE-2019-1010022,https://avd.aquasec.com/nvd/cve-2019-1010022,LOW,libc6,2.36-9+deb12u7,
CVE-2019-1010023,https://avd.aquasec.com/nvd/cve-2019-1010023,LOW,libc6,2.36-9+deb12u7,
CVE-2019-1010024,https://avd.aquasec.com/nvd/cve-2019-1010024,LOW,libc6,2.36-9+deb12u7,
CVE-2019-1010025,https://avd.aquasec.com/nvd/cve-2019-1010025,LOW,libc6,2.36-9+deb12u7,
CVE-2019-9192,https://avd.aquasec.com/nvd/cve-2019-9192,LOW,libc6,2.36-9+deb12u7,
CVE-2023-52426,https://avd.aquasec.com/nvd/cve-2023-52426,LOW,libexpat1,2.5.0-1,
CVE-2024-28757,https://avd.aquasec.com/nvd/cve-2024-28757,LOW,libexpat1,2.5.0-1,
CVE-2022-27943,https://avd.aquasec.com/nvd/cve-2022-27943,LOW,libgcc-s1,12.2.0-14,
CVE-2018-6829,https://avd.aquasec.com/nvd/cve-2018-6829,LOW,libgcrypt20,1.10.1-3,
CVE-2011-3389,https://avd.aquasec.com/nvd/cve-2011-3389,LOW,libgnutls30,3.7.9-2+deb12u3,
CVE-2018-5709,https://avd.aquasec.com/nvd/cve-2018-5709,LOW,libgssapi-krb5-2,1.20.1-2+deb12u2,
CVE-2018-5709,https://avd.aquasec.com/nvd/cve-2018-5709,LOW,libk5crypto3,1.20.1-2+deb12u2,
CVE-2018-5709,https://avd.aquasec.com/nvd/cve-2018-5709,LOW,libkrb5-3,1.20.1-2+deb12u2,
CVE-2018-5709,https://avd.aquasec.com/nvd/cve-2018-5709,LOW,libkrb5support0,1.20.1-2+deb12u2,
CVE-2022-0563,https://avd.aquasec.com/nvd/cve-2022-0563,LOW,libmount1,2.38.1-5+deb12u1,
CVE-2023-45918,https://avd.aquasec.com/nvd/cve-2023-45918,LOW,libncursesw6,6.4-4,
CVE-2022-0563,https://avd.aquasec.com/nvd/cve-2022-0563,LOW,libsmartcols1,2.38.1-5+deb12u1,
CVE-2021-45346,https://avd.aquasec.com/nvd/cve-2021-45346,LOW,libsqlite3-0,3.40.1-2,
CVE-2024-2511,https://avd.aquasec.com/nvd/cve-2024-2511,LOW,libssl3,3.0.13-1~deb12u1,
CVE-2022-27943,https://avd.aquasec.com/nvd/cve-2022-27943,LOW,libstdc++6,12.2.0-14,
CVE-2013-4392,https://avd.aquasec.com/nvd/cve-2013-4392,LOW,libsystemd0,252.26-1~deb12u2,
CVE-2023-31437,https://avd.aquasec.com/nvd/cve-2023-31437,LOW,libsystemd0,252.26-1~deb12u2,
CVE-2023-31438,https://avd.aquasec.com/nvd/cve-2023-31438,LOW,libsystemd0,252.26-1~deb12u2,
CVE-2023-31439,https://avd.aquasec.com/nvd/cve-2023-31439,LOW,libsystemd0,252.26-1~deb12u2,
CVE-2023-45918,https://avd.aquasec.com/nvd/cve-2023-45918,LOW,libtinfo6,6.4-4,
CVE-2013-4392,https://avd.aquasec.com/nvd/cve-2013-4392,LOW,libudev1,252.26-1~deb12u2,
CVE-2023-31437,https://avd.aquasec.com/nvd/cve-2023-31437,LOW,libudev1,252.26-1~deb12u2,
CVE-2023-31438,https://avd.aquasec.com/nvd/cve-2023-31438,LOW,libudev1,252.26-1~deb12u2,
CVE-2023-31439,https://avd.aquasec.com/nvd/cve-2023-31439,LOW,libudev1,252.26-1~deb12u2,
CVE-2022-0563,https://avd.aquasec.com/nvd/cve-2022-0563,LOW,libuuid1,2.38.1-5+deb12u1,
CVE-2007-5686,https://avd.aquasec.com/nvd/cve-2007-5686,LOW,login,1:4.13+dfsg1-1+b1,
CVE-2019-19882,https://avd.aquasec.com/nvd/cve-2019-19882,LOW,login,1:4.13+dfsg1-1+b1,
CVE-2023-29383,https://avd.aquasec.com/nvd/cve-2023-29383,LOW,login,1:4.13+dfsg1-1+b1,
TEMP-0628843-DBAD28,https://security-tracker.debian.org/tracker/TEMP-0628843-DBAD28,LOW,login,1:4.13+dfsg1-1+b1,
CVE-2022-0563,https://avd.aquasec.com/nvd/cve-2022-0563,LOW,mount,2.38.1-5+deb12u1,
CVE-2023-45918,https://avd.aquasec.com/nvd/cve-2023-45918,LOW,ncurses-base,6.4-4,
CVE-2023-45918,https://avd.aquasec.com/nvd/cve-2023-45918,LOW,ncurses-bin,6.4-4,
CVE-2024-2511,https://avd.aquasec.com/nvd/cve-2024-2511,LOW,openssl,3.0.13-1~deb12u1,
CVE-2007-5686,https://avd.aquasec.com/nvd/cve-2007-5686,LOW,passwd,1:4.13+dfsg1-1+b1,
CVE-2019-19882,https://avd.aquasec.com/nvd/cve-2019-19882,LOW,passwd,1:4.13+dfsg1-1+b1,
CVE-2023-29383,https://avd.aquasec.com/nvd/cve-2023-29383,LOW,passwd,1:4.13+dfsg1-1+b1,
TEMP-0628843-DBAD28,https://security-tracker.debian.org/tracker/TEMP-0628843-DBAD28,LOW,passwd,1:4.13+dfsg1-1+b1,
CVE-2011-4116,https://avd.aquasec.com/nvd/cve-2011-4116,LOW,perl-base,5.36.0-7+deb12u1,
CVE-2023-31486,https://avd.aquasec.com/nvd/cve-2023-31486,LOW,perl-base,5.36.0-7+deb12u1,
TEMP-0517018-A83CE6,https://security-tracker.debian.org/tracker/TEMP-0517018-A83CE6,LOW,sysvinit-utils,3.06-4,
CVE-2005-2541,https://avd.aquasec.com/nvd/cve-2005-2541,LOW,tar,1.34+dfsg-1.2+deb12u1,
TEMP-0290435-0B57B5,https://security-tracker.debian.org/tracker/TEMP-0290435-0B57B5,LOW,tar,1.34+dfsg-1.2+deb12u1,
CVE-2022-0563,https://avd.aquasec.com/nvd/cve-2022-0563,LOW,util-linux,2.38.1-5+deb12u1,
CVE-2022-0563,https://avd.aquasec.com/nvd/cve-2022-0563,LOW,util-linux-extra,2.38.1-5+deb12u1,lities.csv…]()




## Задача 3
1. Изучите файл "proxy.yaml"
2. Создайте в репозитории с проектом файл ```compose.yaml```. С помощью директивы "include" подключите к нему файл "proxy.yaml".
3. Опишите в файле ```compose.yaml``` следующие сервисы: 

- ```web```. Образ приложения должен ИЛИ собираться при запуске compose из файла ```Dockerfile.python``` ИЛИ скачиваться из yandex cloud container registry(из задание №2 со *). Контейнер должен работать в bridge-сети с названием ```backend``` и иметь фиксированный ipv4-адрес ```172.20.0.5```. Сервис должен всегда перезапускаться в случае ошибок.
Передайте необходимые ENV-переменные для подключения к Mysql базе данных по сетевому имени сервиса ```web``` 

- ```db```. image=mysql:8. Контейнер должен работать в bridge-сети с названием ```backend``` и иметь фиксированный ipv4-адрес ```172.20.0.10```. Явно перезапуск сервиса в случае ошибок. Передайте необходимые ENV-переменные для создания: пароля root пользователя, создания базы данных, пользователя и пароля для web-приложения.Обязательно используйте уже существующий .env file для назначения секретных ENV-переменных!

2. Запустите проект локально с помощью docker compose , добейтесь его стабильной работы: команда ```curl -L http://127.0.0.1:8090``` должна возвращать в качестве ответа время и локальный IP-адрес. Если сервисы не стартуют воспользуйтесь командами: ```docker ps -a ``` и ```docker logs <container_name>``` 

5. Подключитесь к БД mysql с помощью команды ```docker exec <имя_контейнера> mysql -uroot -p<пароль root-пользователя>```(обратите внимание что между ключем -u и логином root нет пробела. это важно!!! тоже самое с паролем) . Введите последовательно команды (не забываем в конце символ ; ): ```show databases; use <имя вашей базы данных(по-умолчанию example)>; show tables; SELECT * from requests LIMIT 10;```.

6. Остановите проект. В качестве ответа приложите скриншот sql-запроса.

## Задача 4
1. Запустите в Yandex Cloud ВМ (вам хватит 2 Гб Ram).
2. Подключитесь к Вм по ssh и установите docker.
3. Напишите bash-скрипт, который скачает ваш fork-репозиторий в каталог /opt и запустит проект целиком.
4. Зайдите на сайт проверки http подключений, например(или аналогичный): ```https://check-host.net/check-http``` и запустите проверку вашего сервиса ```http://<внешний_IP-адрес_вашей_ВМ>:8090```. Таким образом трафик будет направлен в ingress-proxy.
5. (Необязательная часть) Дополнительно настройте remote ssh context к вашему серверу. Отобразите список контекстов и результат удаленного выполнения ```docker ps -a```
6. В качестве ответа повторите  sql-запрос и приложите скриншот с данного сервера, bash-скрипт и ссылку на fork-репозиторий.

## Задача 5 (*)
1. Напишите и задеплойте на вашу облачную ВМ bash скрипт, который произведет резервное копирование БД mysql в директорию "/opt/backup" с помощью запуска в сети "backend" контейнера из образа ```schnitzler/mysqldump``` при помощи ```docker run ...``` команды. Подсказка: "документация образа."
2. Протестируйте ручной запуск
3. Настройте выполнение скрипта раз в 1 минуту через cron, crontab или systemctl timer. Придумайте способ не светить логин/пароль в git!!
4. Предоставьте скрипт, cron-task и скриншот с несколькими резервными копиями в "/opt/backup"

## Задача 6 (*)
Скачайте docker образ ```hashicorp/terraform:latest``` и скопируйте бинарный файл ```/bin/terraform``` на свою локальную машину, используя dive и docker save.
Предоставьте скриншоты  действий .

## Задача 6.1
Добейтесь аналогичного результата, используя docker cp.  
Предоставьте скриншоты  действий .

## Задача 6.2 (**)
Предложите способ извлечь файл из контейнера, используя только команду docker build и любой Dockerfile.  
Предоставьте скриншоты  действий .

## Задача 7 (***)
Запустите ваше python-приложение с помощью runC, не используя docker или containerd.  
Предоставьте скриншоты  действий .
