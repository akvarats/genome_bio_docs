# Справка по командам cli

- [Первоначальные настройки](#первоначальные-настройки)
- [Команды CLI](#команды-cli)
    - [Общие команды](#общие-команды)
    - [Команды для разработчика](#команды-для-разработчика)
    - [Команды для работы с пайплайнами](#команды-для-работы-с-пайплайнами)

## Первоначальные настройки

План настроек:

1. Установка python и CLI + зависимости;
2. Настройка соединения с мастером Биоинформатики;
3. Регистрация

### Установка

1. Устанавливаем python версии 3 или выше;
2. Клонируем репозиторий https://github.com/akvarats/genome_bio_cli
   (`git clone git@github.com:akvarats/genome_bio_cli.git`)
3. В папке репозитория выполняем скрипт `./install`

### Соединение с мастером

Для

```sh
$ ./bio master connect --url %MASTER_URL%
```

## Команды CLI

Список доступных команд их параметров можно узнать прямо в командной
строке:

```
$ ./bio --help

Usage: bio.py [OPTIONS] COMMAND [ARGS]...

  Интерфейс командной строки для модуля "Биоинформатика" (с) Геном-Эксперт
  2020

Options:
  --help  Show this message and exit.

Commands:
  dev       Инструменты разработчика
  master    Запросы к мастеру био-информатики
  pipeline  Работа с пайплайнами (запуск, получение статуса, результаты)
```

```sh
$ ./bio dev --help

Usage: bio.py dev [OPTIONS] COMMAND [ARGS]...

  Инструменты разработчика

Options:
  --help  Show this message and exit.

Commands:
  add-key          Добавление ssh ключа для доступа к хранилищу
  check-pipeline   Проверка локального пайплайна
  clone-pipeline   Клонирование репозитория с пайплайном в локальную папку
  create-pipeline  Создание нового репозитория с пайплайном
  images           Просмотр списка доступных образов
  pipelines        Просмотр списка доступных пайплайнов
  push-image       Отправка образа в реестр биомастера
  run-pipeline     Локальный запуск пайплайна (для отладочных целей)


$ ./bio dev clone-pipeline --help

.. и т.д
```

### Общие команды

**`master connect`** 

Команда для установки соединения с мастером биоинформатики.

Параметры:

* `--url / -u` - URL к биомастеру;

Пример:

```
$ ./bio master connect --url 192.168.5.10:50000
```

**`master about`**

Получение информации о текущей конфигурации мастера биоинформатики.

Пример:

```
$ ./bio master about
```

### Команды для разработчика

**`dev add-key`**

Добавление ключа разработчика (для доступа к хранилищу пайплайнов).

Параметры:

* `--key / -k` - значение ключа (которое можно получить, например, так: `cat ~/.ssh/id_rsa.pub`). Указывается в двойных кавычках, т.к. внутри содержит пробелы.

Пример:

```
$ ./bio dev add-key --key "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC2zd8CjNiGvDFTN395Cj/Qdb1OkqGfZogOlmDsjXGz46tNedq06Sw0xnUHskWKDi3jQNjMWrVRXBW6UlwInKzyPuQ2lmHO2bLwa2tk6BOSzXJvSGYLDLA1pe/ZIKz4ErU5nuu+Czl2R/VpTSMpT2e3maWWB+5Up3Od1AwAqQKTsbpgAGwstE9if/uWlYVAgqmOOzY/JSbEUHZBa7ArN4bfwKmGZA0TkwKVpy32mecjqSiUMDz+mx1pUd+KPFNux9cbMcHwtyRp5ehL3Ioyw5LYaZQhYdS3et7mRdKHaRGHc4FtI3leQn8fpgVLrB/PzNJrQAt/YuT3xrevwtvukfT5 akvarats@akvarats-hp"
```

**`dev pipelines`**

Получение списка доступных пайплайнов.

Пример:

```
$ ./bio dev pipelines
```

**`dev create-pipeline`**

Создает новый пайплайн в хранилище.

Параметры:

* `--name / -n` - наименование пайплайна. 

**Важное замечание**: наименование пайплайна указывается в сокращенном варианте (без префикса пользователя). То есть, если команда `./bio dev pipelines` возвращает полные названия пайплайнов (вида `genome/my_pipeline`), то при создании пайплайна префикс пользователя (`genome/`) не указывается (он будет добавлен автоматически).

Пример:

```sh
$ ./bio dev create_pipeline --name my_pipeline
```

### Команды для работы с пайплайнами

