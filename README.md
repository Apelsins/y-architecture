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
2) auth-microfrontend - 8080
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

 2) 
 /profile-microfrontend - 8081
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

3) main-microfrontend - 8082  
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

4) display-board-microfrontend - 8083
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

5) operation-board-microfrontend - 8084
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