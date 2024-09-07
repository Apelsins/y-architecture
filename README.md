# Задание 1

### Я бекенд разработчик на джаве, фронт знаю плохо, поэтому не буду выполнять все 3 подзадания, а выполню лишь необходимое.

### Предлагаю разбить фронт на 5 микрофронтендов:
1) auth-microfrontend - отвечает за вход и регистрацию пользователей. 
2) profile-microfrontend - отвечает за отоброжение профиля и его редакитрование.
3) main-microfrontend - отвечает за главную страницу и взаимодействия между display-board-microfrontend и operation-board-microfrontend
4) display-board-microfrontend - отвечает за отоброжение фотографий. 
5) operation-board-microfrontend - отвечает за добавление/удаление фотографий, лайки

### Некоторые мои соображения и взаимодействие:
1) Пользователь в начале попадает в auth-microfrontend. После авторизации попадает на main-microfrontend.
2) profile-microfrontend и display-board-microfrontend одновременно отображены на страничке и принадлежат main-microfrontend.
3) При добавление/удаление фотографий микрофронтенд operation-board-microfrontend асинхронно уведомляет display-board-microfrontend.
5) Здесь я не уверен, но я не стал создавать микрофроденд foto-microfrontend(сard), думаю совокупность фотографий, а именно display-board-microfrontend, лучшее решение в данной ситуации. Если фронт будет осложняться дальше, то можно ввести foto-microfrontend как контейнер низкого уровня.

## Структуры проекта для каждого микрофронтенда:
### 1) auth-microfrontend - 8080
```
/auth-microfrontend
  /src
    /components
      InfoTooltip.js         // Информация, если вход неуспешен
      Login.js               // Компонент входа пользователя
      Register.js            // Компонент регистрации пользователя
    /styles
      login.css              // Стили для компонента входа
      register.css           // Стили для компонента регистрации
    /utils
      auth.js                // Утилиты для аутентификации
    index.js                 // Точка входа микрофронтенда
  package.json               // Зависимости и скрипты микрофронтенда
  webpack.config.js
```

### 2) /profile-microfrontend - 8081
```
  /src
    /components
      EditAvatarPopup.js     // Компонент изменения аватара
      EditProfilePopup.js    // Компонент изменения профиля
    /styles
      profile__add-button.css   // Стили для профайла
      profile__description.css
      edit-buttom.css
      profile__image.css
      profile__info.css
      profile__titile.css
      profile__profile.css           
    index.js                 // Точка входа микрофронтенда
  package.json               // Зависимости и скрипты микрофронтенда
  webpack.config.js 
```

### 3) main-microfrontend - 8082  
```
  /src
    /components
      App.js                // Основной копонент 
      CurrentUserContext.js // в main будет хранится контекст
      Footer.js             
      Header.js
      Main.js               // main будет отвечать за api
      ProtectedRoute.js     // будет отвечать за маршрутизацию
    /styles
      header-user.css       // Стили для main
      header-user_wrapper.css
      header.css
      popup_label.css
      popup.css          
    index.js                 // Точка входа микрофронтенда
  package.json               // Зависимости и скрипты микрофронтенда
  webpack.config.js 
```

### 4) display-board-microfrontend - 8083
```
  /src
    /components
      Card.js                // Компонент, где хранится фото
      ImagePopup.js          // Комонент для взаимодействия с фото
    /styles
      card-description.css       // Стили для display-board-microfrontend
      card_image.css
      card.css
      content.css
    index.js                 // Точка входа микрофронтенда
  package.json               // Зависимости и скрипты микрофронтенда
  webpack.config.js 
```

### 5) operation-board-microfrontend - 8084
```
  /src
    /components
      AddPlacePopup.js          // Компонент, добаялется/удаляется картинка
      Like.js                   // Добавление лайка
      PopupWithForm.js          // Сохранение картинки
    /styles
      card_like-buttom.css   // Стили для operation-board-microfrontend
      popup.css
    index.js                 // Точка входа микрофронтенда
  package.json               // Зависимости и скрипты микрофронтенда
  webpack.config.js   
  ```


# Задание 2
## Это задание гораздо важней для меня, чем первое. Укажите пожалуйста на грубые ошибки. 
## Файл result.drawio лежит в draw\result.drawio в проекте. Если нужно куда-то в другое место убрать, напишите.
## Я открываю файл онлайн с гитхаба, опять же, если нужно по другому загрузить, напишите.

## Я разбил монолит на следующие микросервисы:
### 1) Авторизация
Сервис будет хранить id пользователя, генерировать JWT токен, будет взаимодействовать с keykloak.
Будет своя база данных, в которой будет хранится информация о времени и кол-ве авторизаций пользователей.

### 2) Личный кабинет пользователя
Будет хранится личная информация о пользователе, а также возможность изменить эту информацию.

### 3) Нотификация
Отвечает за отправку сообщений по почте/telegram/sms. Не стал делать свою БД, но вполне моджно сделать, если планируется сложная логика.
Ниже указал kafka, как брокер сообщений. Подразумевается, что будет применена событийная модель, сервисы будут отправлять события в сервис через kafka.

### 4) Заказ

### 5) Аукцион

### 6) Корзина товаров/услуг
Тут решил не разделять на 2 сервиса, хотя и можно. Думаю товары и услуги слишком тесно связаны и имеют очень много общего.
Может и ошибочное мнение у меня. Хотя и попахивает монолитом, но считаю уж слишком близкие вещи не стоит делить.

Будет своя БД, в которой будух хранится товары и услуги.
 
### 7) Апелляция

### 8) Техподдержка
Будет выделенным сервисом между поддержкой и остальными сервисами.

### 9) Отчетность
Часто пользователям нужно будет выгружать различные документы, отчеты. Сделаем для этого отдельный сервис.
БД будет документно-ориентированной, например, MongoDB. Будем там хранить все отчеты для историчноти.

### 9) Микросервис: платежный сервис
Будет отдельный микросервис для взаимодействия с внешним платежный сервис. Нужно будет как-то валидировать данные.
Можно реализовать паттерн Circuit Breaker, может каждое обращение к платежному сервису стоит денег.

### 9) Оркестратор(SAGA) 
Предлагаю использовать Оркетратор для операций, которые будут использовать несколько сервисов. 
Хареография подойдет в меньшей степени, потому что некоторые операции могут затрагивать более 5 сервисов. И с помощью хареографии будет тяжелей поддреживать.  


## Между микросервисами будет много взаимодествий, не буду описывать все. Опишу только примеры длинных транзакций, которые затрагивают несколько сервисов сразу. Также не буду все это рисовать, если надо, скажите, просто куча стрелок ухудшит читаемость схемы.

### 1) Транзакция: регистрация нового пользователя а также добавления ему сразу несколько бесплатных услуг.
Шаги:
1) С фронта приходят данные о пользователе
2) Создается транзакция в оркестраторе
3) Оркестратор добавляет пользователя в сервисе Авторизация
4) Оркестратор добавляет данные о пользователе в Линый кабинет пользователя
5) Оркестратор добавляет услуги в Корзина товаров/услуг
6) Оркестратор отправляет событие в сервис Нотификация
7) Если что-то происходит не так, то происходят компенсирующие транзакции 

### 2) Транзакция: оплата тавара.
Шаги:
1) С фронта приходят данные об оплате
2) Проходит авторизация
3) Создается транзакция в оркестраторе
4) Оркестратор идет в сервис Линый кабинет и смотрит, вдруг пользователь не может купить эти товары.
5) Оркетратор резервирует товар в сервисе Корзина товаров/услуг
6) Оркестратор идет в сервис Взаимодействие с внешним платежным сервисом
7) Сервис Взаимодействие с внешним платежным сервисом взаимодействует с внешним сервисом
8) Оркетратор удаляет/помечает товар в сервисе Корзина товаров/услуг
9) Оркестратор отправляет событие в сервис Нотификация
10) Если что-то происходит не так, то происходят компенсирующие транзакции 
11) Отправляется сообщение фронту


## Если все же надо рисовать стрелочки, то нарисую. Просто куча времени на это тратить, хотя я все описал в тексте.



 