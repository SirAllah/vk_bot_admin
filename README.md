# vink

Бот администратор для беседы вк на Callback API.

* [Команды](#Команды)
  * [Администратора](#Администратора)
  * [Владельца](#Владельца)
* [Настройка бота](#Настройка-бота)
* [Настройка запросов](#Настройка-запросов)

## Команды

### Администратора

Команды доступные всем администраторам беседы.

#### кик
*  Исключает заданных участников из беседы. 

   **Пример:** `кик *user1`
   
#### бан
*  Исключает заданных участников из беседы и записывает их id в чёрный список. 

   **Пример:** `бан *user1`

#### анбан
*  Удаляет id заданных участников из чёрного списка. 

   **Пример:** `анбан *user1`
   
#### варн
*  Выдает предупреждение заданным участникам. 

   **Пример:** `варн *user1`
   
#### анварн
*  Снимает все предупреждения с заданных участников. 
 
   **Пример:** `анварн *user1`
   
#### !банворды
*  Выводит список слов из чёрного списка.

   **Пример:** `!банворды`

### Владельца

Команды доступные только владельцу бота.

#### повысить
*  Выдает роль администратора заданным участникам. 
 
   **Пример:** `повысить *user1`
   
#### понизить
*  Снимает роль администратора с заданных участников. 
 
   **Пример:** `понизить *user1`
   
#### !варн
*  Изменяет количество варнов до исключения. 
 
   **Пример:** `!варн 5`

#### !приветствие
*  Изменяет приветствие при присоединении новых пользователей. 
 
   **Пример:** `!приветствие Добро пожаловать`
   
#### +ссылки
*  Разрешает отправку ссылок в беседе. 
 
   **Пример:** `+ссылки`

#### -ссылки
*  Запрещает отправку ссылок в беседе. 
 
   **Пример:** `-ссылки`
   
#### +банворд
*  Добавляет указанные слова в чёрный список.
 
   **Пример:** `+банворд аниме`
   
#### -банворд
*  Удаляет указанные слова из чёрного списка.
 
   **Пример:** `-банворд аниме`

Все команды с упоминанием / ссылкой на страницу можно использовать сразу для нескольких участников:

<p align="left">
  <a href="">
    <img src="https://raw.githubusercontent.com/FallenAstaroth/vink/master/docs/1.jpg" style="display: inline-block;">
  </a>
</p>

А также смешывать упоминания со ссылками и ответом на сообщение:

 <p align="left">
  <a href="">
    <img src="https://raw.githubusercontent.com/FallenAstaroth/vink/master/docs/2.jpg" style="display: inline-block;">
  </a>
</p>

## Настройка бота

Заполняем поля файла `config.py`:

  * `token` - токен бота.
  * `confirmation_token` - строка, которую должен вернуть сервер.
  * `bot_id` - айди бота.
  * `owner` - айди владельца.
  * `host` - адрес сервера.
  * `port` - порт сервера.

Для получения токена бота переходим в нужную группу:
```
Управление
-> Настройки
-> Работа с API
   * Создать ключ
-> Выставляем галочки и создаем
```
`confirmation_token` находится в этом же разделе, во вкладке Callback API.

Для получения айди бота переходим в нужную группу:
```
-> Управление
-> Настройки
   * Адрес
   * Номер сообщества
   * club*цифры*
-> Копируем только цифры
```

После заполнения `config.py`: 

1. Заливаем бота на свой сервер.
2. Устанавливаем зависимости:
```
pip install -r requirements.txt
```
3. Запускаем `bot.py`.

Разрешаем добавлять бота в беседы:
```
-> Управление
-> Сообщения
   * Сообщения сообщества: Включены
-> Настройки для бота
   * Возможности ботов: Включены
   * Разрешать добавлять сообщество в беседы - ставим галочку
```

Настройка Callback API:
```
-> Управление
-> Настройки
-> Работа с API
-> Callback API
   * Версия API: 5.131
   * Адрес: ссылка на ваш сервер с ботом
   * Нажимаем "Подтвердить"
-> Типы событий
   * Выставляем галочки
```
## Настройка запросов

Если у вас белый (внешний) IP адрес, то в `config.py` вставляем его в поле `host`, делаем пробрасывание желаемого порта и вставляем в поле `port`. Как это сделать можно найти в интернете.

Если же у вас серый (частный) IP адрес, то придется использовать дополнительное программное обеспечение.

Пример использования с **Ngrok**:
1. [Регистрируем](https://ngrok.com/signup) аккаунт.
2. [Скачиваем](https://ngrok.com/download) Ngrok.
3. Копируем токен авторизации с [личного кабинета](https://dashboard.ngrok.com/get-started/your-authtoken).
4. Открываем Ngrok.
5. Сохраняем токен при помощи команды (без треугольных скобок). Это делается только один раз, чтобы снять ограничение по времени работы:
```
ngrok authtoken <токен>
```
6. Запускаем командой:
```
ngrok http 8080
```
7. Копируем вторую ссылку `Forwarding` до `-> http://localhost:8080`.
8. Запускаем бота.
8. Вставляем ссылку из `Forwarding`:
```
-> Управление
-> Настройки
-> Работа с API
-> Callback API
   * Адрес: ссылка из Forwarding
   * Нажимаем "Подтвердить"
```
9. Тестим.

Важно не закрывать **Ngrok** при работе бота.
