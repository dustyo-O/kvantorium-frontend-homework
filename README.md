## Домашняя работа по теме "frontend разработка"

### Задача
Разработайте приложение для прохода на фантазийное мероприятие. Например, на новогодний корпоратив "Кванториум". 
Приложение имеет два интерфейса:
- получение QR кода
- проверка QR кода контроллером

и один бекэнд, с которым оба интерфейса взаимодействуют

#### Получение QR кода
Сделайте простую веб-страницу, на которой только один обязательный элемент - кнопка "получить билет". В остальном, не сдерживайте себя, сделайте настолько привлекательный лендинг, насколько захотите. Можете постараться сделать по-настоящему приятное приглашение опираясь на сервисы, которые вам нравятся. Но не переживайте - просто кнопка на белом фоне тоже 👌

**Базовая функциональность**

Кнопка должна работать следующим образом - после ее нажатия пользователь должен получить готовый QR код (картинку). Лучше, если браузер сразу начнет скачивать картинку. Постарайтесь, чтобы одного клика для получения QR кода было достаточно – это очень порадует пользователей.

**Варианты реализации, подсказки и советы**

Кнопка по нажатию должна работать так - запросить GET запросом новый токен у бекэнда. На клиенте сформировать из токена картинку и отдать ее пользователю. Чтобы начать скачивание - вам надо создать ссылку на картинку (вам поможет "виртуальный" URL https://developer.mozilla.org/ru/docs/Web/API/URL/createObjectURL) и программно кликнуть по ссылке

В принципе, никто не мешает сформировать картинку и на бекэнде, но передать и токен, и картинку под него - это точно путь усеянный болью, хотя и возможный.

Так или иначе, для формирования QR кода понадобится сторонняя библиотека - это нормально, найдите ее в npm.

#### Проверка QR кода
Мы предполагаем, что на проверке билетов будет стоять человек с телефоном, подключенным к мобильному интернету. Надо сделать страницу с кнопкой "проверить", которая будет инициализировать камеру. Получив изображение с камеры, мы должны считать с него токен, и определить, действителен ли билет. В зависимости от результатов проверки следует явно дать знать о результатах - чем ярче это будет, тем лучше, например, можно весь фон страницы красить в зеленый/красный оттенок - ну или любой другой способ, какой подскажет фантазия. Мы предполагаем, что перед контролером будет большая очередь, поэтому чем удобнее и быстрее будет проверка билетов, тем лучше. 

**Базовая функциональность**

Интерфейс снова с одним интерактивным элементом (кнопкой?), нажатие на которую приводит к активации камеры (после того как оператор даст соответствующее разрешение). Получив картинку, на клиенте "прочитайте" токен с QR кода. Если токен не прочитан, хорошо бы сообщить об этом в интерфейсе. Прочитанный токен проверяем, и если он действительный - отражаем это в интерфейсе

**Варианты реализации, подсказки и советы**

Читать токен из картинки проще на клиенте - у нас там есть все для чтения содержимого картинки. Подойдет FileReader, который мы смотрели на занятии, также можете попробовать подружить видео с canvas - или даже использовать для того, чтобы делать фото готовый модуль - их тоже очень много по запросам в поиск.

Вы можете пробовать считать содержимое картинки на сервере - но это тоже путь воина (сложнее), давайте считать что мы обеспечим контроллера мощным устройством, которое не будет тупить с обработкой изображений.

Прочитанный токен надо проверить с помощью бекэнда. Отправьте токен на бекэнд - можно любым типом запроса, хотя грамотнее будет POST (но если пока сложно, обычный GET запрос не будет ошибкой). Бекэнд пусть ответит JSONом со статусом токена, и удалит токен из хранилища (в качестве хранения - можно складывать даже просто в переменную, или можно использовать jsonы, если хотите чтобы все не обнулялось при падении сервера).

### Бекэнд
Должен иметь две ручки - 
 - для сохранения токена
 - для проверки токена

можно хранить токены прямо в переменной. После проверки погашенный токен удаляем.

**Варианты реализации, подсказки и советы**

Если будете передавать данные в теле POST-запроса, получить данные поможет http://expressjs.com/en/resources/middleware/body-parser.html (если у вас express). Если вы решите поднять все на встроенном http-сервере, то да поможет вам бог:)


### Архитектура
Подойдет реализация на любом наборе технологий. Будет лучше, если вы сможете задеплоить приложение куда-либо, чтобы можно было проверить функциональность. Если не получится, дайте необходимые инструкции по локальной установке (или приходите за помощью по деплою)
