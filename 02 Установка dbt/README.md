# Установка dbt и разворот учебного проекта на локальном компьютере

## Этап 1. Установка python, если он не установлен

#### Шаг 1. Скачиваем дистрибутив с [официального сайта python](https://www.python.org/downloads/)
#### Шаг 2. Запускаем установку из дистрибутива.
При установке на ОС Windows поставьте галочку в пункте "Add python.exe to PATH":

![image](https://github.com/user-attachments/assets/e8199c37-3d2a-400d-bd0a-91a190e2e843)
#### Шаг 3. Проверяем установку.
Откройте PowerShell или окно Терминала и выполните команду 

````console
# Windows
python --version
````
````console
# Mac OS
python3 --version
````

Вы должны увидеть сообщение похожее на:
![image](https://github.com/user-attachments/assets/1b714705-c91a-4905-b5c5-f2af08729317)

## Этап 2. Установка git, если не установлен

#### Шаг 1. Скачать дистрибутив с [официального сайта git](https://git-scm.com/downloads).
#### Шаг 2. Установить git из скачанного дистрибутива.

## Этап 3. Скачивание учебного проекта

#### Шаг 1. Скачиваем код проекта
Откройте терминал и перейдите в папку, в которую хотите скачать проект.
Выполните команду:
````console
git clone https://github.com/amelinvladimir/dbt_course.git
````

## Этап 4. Установка DBeaver (если не установлен)

Смотри в первом этапе [инструкции](https://github.com/amelinvladimir/sql_course/blob/main/%D0%A3%D1%80%D0%BE%D0%BA%201.2%20%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0%20%D0%9F%D0%9E/README.md)


## Этап 5. Установка Docker Desktop (если не установлен)

### На Windows
[Инструкция по установке](https://github.com/amelinvladimir/docker_course/blob/main/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0%20Docker%20%D0%BD%D0%B0%20Windows%2010/README.md)
### На Mac OS
[Инструкция по установке](https://github.com/amelinvladimir/docker_course/blob/main/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0%20Docker%20%D0%BD%D0%B0%20Mac%20OS/README.md)

## Этап 6. Запуск контейнера с БД учебного проекта

#### Шаг 1. Открыть терминал или powershell
#### Шаг 2. Выполнить команду запуска образа

````console
docker run --name dbt-course-postgres -e POSTGRES_PASSWORD=mysecretpassword -p 4001:5432 -d amelinvd/dbt_course_postgres_db_multiplatform
````

Запасной, если первый не сработает:
````console
docker run --name dbt-course-postgres -e POSTGRES_PASSWORD=mysecretpassword -p 4001:5432 -d amelinvd/dbt_course_postgres_db
````

СУБД запущена. С помощью DBeaver можно подключиться к БД, используя следующие параметры
````console
тип БД: PostgreSQL
host: localhost
port: 4001
Имя БД: postgres
login: postgres
password: mysecretpassword
````
Поставить галочку в поле "Показать все базы данных"

## Этап 7. Создать файл profiles.yml с указанием параметров подключения к БД для dbt

#### Шаг 1. Открыть терминал или powershell
#### Шаг 2. Создать файл profiles.yml, выполнив команду:
````console
# Mac OS
touch ~/.dbt/profiles.yml

# Win PowerShell
New-Item ~/.dbt/profiles.yml
````
#### Шаг 3. Открыть на редактирование файл, выполнив команду:
````console
# Mac OS
nano ~/.dbt/profiles.yml

# Win PowerShell
notepad.exe profiles.yml
````
#### Шаг 4. Указать параметры подключения к БД

скопировать текст:
````console
dbt_course:
  outputs:
    dev:
      dbname: dbt_course
      host: localhost
      pass: mysecretpassword
      port: 4001
      schema: bookings_dbt
      threads: 4
      type: postgres
      user: postgres
  target: dev
````

##### Для Mac OS
В окне терминала последовательно нажать следующие комбинации клавиш:
````console
Ctrl + V # вставить текст
Ctrl + O # сохранить
Enter # подтвердить путь сохранения
Ctrl + X # выйти
````

##### Для Windows
Вставить текст в блокноте, сохранить и закрыть текстовый редактор.



## Этап 8. Установка Visual Studio Code (VS Code), если не установлен

#### Шаг 1. Скачиваем дистрибутив с [сайта](https://code.visualstudio.com/) и запускаем установку.
#### Шаг 2. При устанвоке оставляем все настройки по умолчанию (или делайте изменения по своему усмотрению).
#### Шаг 3. Запускаем Visual Studio Code.
![image](https://github.com/user-attachments/assets/23d4ada8-1426-4694-b747-9f3267169dd4)
#### Шаг 4. Открываем папку проект.
Выбрать пункт меню "Файл -> Открыть папку" и выбрать папку dbt_course/dbt_course/ проекта, скачанного с git.
Вы должны увидеть в меню слева следующие папки и файлы:

![image](https://github.com/user-attachments/assets/21c5c528-3d99-413a-a425-8699333b74ab)

## Этап 9. Установить расширение "Power User for dbt" в Visual Code

#### Шаг 1. Нажать на шестиренку в левом нижнем углу и выбрать пункт "Расширения"
#### Шаг 2. В открывшейся строке поиска введите "Power User for dbt" и нажмите на соответствующий появившейся плагин. Нажмите "Установить"

![image](https://github.com/user-attachments/assets/aa4725b4-cf88-4796-877e-6f4fe16c194b)


![image](https://github.com/user-attachments/assets/3af73581-a7e6-4623-b7db-f195578acee8)

#### Шаг 3. Если плагин запросит выбрать версию python, то выберите последнюю установленную версию.

## Этап 10. Установить расширение "Python" в Visual Code

#### Шаг 0. Проверка, установлено ли расширение
Нажать на шестиренку и затем выбрать пункт "Расширения" ("Extensions").
![image](https://github.com/user-attachments/assets/e0a5713a-937d-4233-a4a4-2c5cc937fd5d)

Нажмите троеточие рядом с заголовком  "Расширения" ("Extensions") и выберите пункт "Show Running Extensions" ("Показать Запущенные Расширения")
![image](https://github.com/user-attachments/assets/0235d69f-3cc5-4db2-bb98-7ac67601bd2d)

Ищем в открывшемся окне расширение с названием "Python". Если находим, то следущие шаги данного этапа пропускаем.
![image](https://github.com/user-attachments/assets/6f1b3e60-96ba-4a98-b760-3db2f787ef47)

#### Шаг 1. Нажать на шестиренку в левом нижнем углу и выбрать пункт "Расширения" ("Extensions")
#### Шаг 2. В открывшейся строке поиска введите "Python" и нажмите на соответствующий появившейся плагин. Нажмите "Установить" ("Install")
Если вы не видите 

## Этап 11. Создать виртуальное окружение "Python" в Visual Code

#### Шаг 1. Открываем расширение Python
##### На Windows
Жмем комбинацию клавиш ctrl+shft+P.
В открывшемся окне введите "Python: select interpreter".
Нажмите на найденный пункт с соответствующим названием.
![image](https://github.com/user-attachments/assets/f80152ad-7026-4ae6-930c-34f7e9789f36)

##### На Mac OS
![image](https://github.com/user-attachments/assets/c91241b6-4626-4ca8-a0e0-0cc896b3c163)

Раскрываем список "Global" и видим все версии Python, установленные на ПК
![image](https://github.com/user-attachments/assets/906dc532-dcff-4d62-9663-a438a6d57075)

#### Шаг 2. Создать новое виртуальное окружение python и выбрать его использование по умолчанию в проекте
##### На Windows
Жмем на пункт "Create virtual environment"
![image](https://github.com/user-attachments/assets/564d32b8-430d-464f-a0dd-20d58a9cf7fe)

Выбираем venv
![image](https://github.com/user-attachments/assets/153eea69-332e-48cf-b77a-3d6409cd2f1c)

Выбираем "Delete and recreate" или "Create"
![image](https://github.com/user-attachments/assets/95c51113-3e92-464c-bb72-7e982f3640ee)

Выбираем версию python
![image](https://github.com/user-attachments/assets/b6998893-778f-4989-86fb-1817ebc5f617)

Ставим галочку рядом с файлом requirements и жмем ОК
![image](https://github.com/user-attachments/assets/93427c14-9411-43fb-933c-01e4dfb36905)

##### На Mac OS
В окне расширения "Python" жмем на плюс в строке "Venv"

![image](https://github.com/user-attachments/assets/01909362-0f6f-421d-b46a-dae5f0217b52)

Жмем на версию python, в которой хотим создать виртуальное окружение
![image](https://github.com/user-attachments/assets/3be1ed61-d0e6-44ee-9e96-524aa045fb6b)

Виртуальное окружение появится в списке расширения "Python". Жмем на звезду рядом с расширением 
![image](https://github.com/user-attachments/assets/39a4ebe2-2d8b-4cf4-b3a3-168024766112)

#### Шаг 3. Устанавливаем dbt для работы с postgres

Открываем терминал 
![image](https://github.com/user-attachments/assets/ca1ef146-21ac-406d-94fa-cbd1c4742206)

````console
# Windows
python -m pip install dbt-postgres
````
при установке на Windows может понадобится дополнительно вызвать команду 
````console
python.exe -m pip install --upgrade pip
````

````console
# Mac OS
python3 -m pip install dbt-postgres
````

Если при установке возникает ошибка, то попробуйте:
* Установить python более ранних версий (замечено, что есть проблемы с python 3.13.*, но на 3.12.* и 3.11.* устанавливается);
* Установите postgresql локально;

#### Шаг 4. Проверяем корректность установки dbt в данной версии Python
Перезапускаем VS Code.
Открываем окно терминала с powershell в Windows и zsh в Mac OS.

В окне терминала выполняем команду 

````console
dbt --version
````

Если увидим сообщение, как на скриншоте с выводом версии dbt библиотеки, то этап успешно завершен
![image](https://github.com/user-attachments/assets/b05d4c45-3aa9-46ed-921e-4bf318fd9284)


Если видим ошибку, как на скриншоте, то выполняем следующий шаг 
![image](https://github.com/user-attachments/assets/ac77cc6a-3d35-4aad-9505-f537545f4e20)

Выполняем команду 
````console
# На Windows
python -m pip install dbt-postgres

# На Mac OS
python3 -m pip install dbt-postgres
````

Если при установке возникает ошибка, то попробуйте использовать более младшую версию Python.

Вновь выполним в окне терминала команду и теперь мы должны увидеть номер версии установленного dbt
````console
dbt --version
````

## Этап 12. Выбираем подсветку синтаксиса
Открываем любой sql файл (можно создать).
В правом нижнем углу редактора жмем на выбор языка подсветки.
Жмем "Настройка сопоставления файлов для .sql"

![image](https://github.com/user-attachments/assets/533c57b3-f3e1-4cd4-ac41-96851b5b188d)

Вводим "Jinja SQL" и выбираем выпавший пункт

![image](https://github.com/user-attachments/assets/b3db17c9-eb8d-4f3e-beea-141b08e23186)
