# Первые шаги

VK Mini Apps — это открытая платформа встраиваемых кросс-платформенных приложений, которые расширяют возможности сайта и приложения ВКонтакте. По этой инструкции вы можете создать своё первое мини-приложение.

Краткая инструкция для опытных пользователей.
Видеоуроки и другие полезные материалы.

Как создать первое мини-приложение

Чтобы познакомиться с платформой и опубликовать первое мини-приложение, вам потребуется:

1. Зарегистрировать мини-приложение ВКонтакте.
2. Собрать мини-приложение.
3. Запустить мини-приложение локально и убедиться, что оно работает.
4. Запустить мини-приложение внутри ВКонтакте.
5. Разместить мини-приложение на хостинге.

Инструкция ниже актуальна для любой операционной системы. Для первых шагов знание языка JavaScript не понадобится, но вы должны уметь работать с командной строкой.

Чтобы использовать библиотеки мини-приложений, установите необходимое программное обеспечение.

Регистрация мини-приложения ВКонтакте

Чтобы зарегистрировать мини-приложение ВКонтакте:

1. Войдите во ВКонтакте под своей учётной записью.

    Чтобы пройти аутентификацию ВКонтакте, вам потребуется мобильное приложение для получения кода подтверждения.

2. Откройте страницу Мои приложения и нажмите на кнопку Создать. Откроется форма Создание приложения.

• Укажите название приложения.

    Название приложения может содержать только буквы, цифры, дефисы и пробелы. Название можно изменить в Настройках.

• Выберите платформу — Встраиваемое приложение.

• Добавьте описание.

• Выберите тип — VK Mini Apps.

    Какие ещё приложения можно создать?

• Выберите категорию приложения.

3. Нажмите кнопку Перейти к настройке приложения.
4. Во всплывающем окне Подтверждение действия:

• Нажмите кнопку Получить код. На указанный в окне телефон отправится код подтверждения в SMS или в push-уведомлении мобильного приложения ВКонтакте.

    Все ключевые действия с мини-приложением, например создание или удаление, требуется подтверждать с помощью кода из SMS или push-уведомления. В рамках сессии код требуется вводить только один раз.

• Введите полученный код подтверждения.

• Нажмите кнопку Отправить код.

5. На странице Правила платформы ознакомьтесь с правилами и нажмите кнопку Я соглашаюсь с новыми правилами.

Регистрация приложения завершена. Откроется страница с информацией о приложении и его настройками.

Создание мини-приложения

Чтобы создать мини-приложение с минимальной функциональностью, используйте библиотеку create-vk-mini-app. Функциональность получившегося мини-приложения: отображение двух экранов с простой навигацией и кнопкой, которая показывает стикер. Также к проекту уже подключены все необходимые npm-библиотеки и поддержано несколько систем публикации.

Чтобы создать мини-приложение, вам потребуются:

• Платформа Node.js.

• Терминал. Можно использовать редактор кода, в котором есть командная строка. Пример: VS Code.

1. Перейдите в папку, в которой хотите создать проект своего мини-приложения:

    cd <ПУТЬ_К_ПАПКЕ>

2. Выполните команду, которая создаст проект c именем <MINI_APP_NAME> в вашей папке:

    npx @vkontakte/create-vk-mini-app <MINI_APP_NAME>
   
    Если не указать название проекта вместо <MINI_APP_NAME>, по умолчанию создастся проект mini-app.

    Получаю ошибку на Windows 10 Pro. Что делать?

3. В терминале подтвердите скачивание библиотеки @vkontakte/create-vk-mini-app: введите Y/y или нажмите Enter.

Структура файлов папки проекта после его создания:

.
└── mini-app
├── node_modules
├── public
├── src
├── package-lock.json
├── package.json
├── README.md
└── vk-hosting-config.json

Проект мини-приложения создан.

Для корректной работы необходима библиотека VK Bridge и вызов события инициализации VKWebAppInit в начале кода мини-приложения. Если не вызвать событие, мини-приложение не будет работать.

Запуск мини-приложения локально

Запуск мини-приложения локально потребуется для последующего запуска мини-приложения внутри ВКонтакте.

1. Перейдите в папку проекта мини-приложения:

    cd <MINI_APP_NAME>

2. Запустите мини-приложение:

    npm start

3. Согласитесь на настройки по умолчанию: введите Y/y или нажмите Enter.

Если всё в порядке, вы получите сообщение:

Compiled successfully!
...
Local:            https://localhost:10888
On Your Network:  https://192.168.1.3:10888

На этом этапе мини-приложение представляет собой веб-сервер, работающий на вашем локальном компьютере. Чтобы в этом убедиться, откройте в браузере ссылку: https://localhost:10888.

Запуск мини-приложения внутри ВКонтакте

Чтобы увидеть результат работы мини-приложения, запустите его на своём компьютере и получите ссылку на него. Мы создали библиотеку VK Tunnel, которая берёт на себя все настройки и позволяет отобразить результат работы вашего мини-приложения в интернете.

1. Откройте новое окно терминала и перейдите в папку проекта мини-приложения:

    cd <ПУТЬ_К_ПАПКЕ_MINI_APP_NAME>

2. Установите VK Tunnel:

    npm install @vkontakte/vk-tunnel --include=dev

3. Добавьте в файл package.json скрипт tunnel. Сохраните файл:

    "scripts": {
    ...
    "tunnel": "vk-tunnel --insecure=1 --http-protocol=https --ws-protocol=wss --host=0.0.0.0 --port=10888"
    }

4. Запустите VK Tunnel:

    npm run tunnel

• Получаю ошибку sh: 1: vk-tunnel: Permission denied. Что делать?

• Получаю ошибку Error: Пользователь не является создателем приложения. Что делать?

• Получаю ошибку Error: connect ECONNREFUSED 127.0.0.1:10888. Что делать?

5. В командной строке вы получите ссылку вида: https://oauth.vk.com/code_auth?stage=check&code=cabbedd. Откройте её в браузере, чтобы пройти аутентификацию.
6. Вернитесь в терминал и подтвердите действие в командной строке: введите Y/y или нажмите Enter.

    Если всё в порядке и VK Tunnel запущен, вы получите сообщение со ссылкой на мини-приложение:
    
    open: https://user743784474-nm77vxr2.wormhole.vk-apps.com/
    VK Tunnel отобразил в интернете веб-сервер, работающий на вашем локальном компьютере. После этого можно запустить мини-приложение внутри ВКонтакте.

7. Включите режим разработки и укажите полученную на предыдущем шаге ссылку (https://user743784474-nm77vxr2.wormhole.vk-apps.com/) в поле URL для разработки. То же самое можно сделать для мобильной версии браузера или мобильного приложения.
8. Откройте в браузере ссылку вида vk.com/app<ID>, где <ID> — это идентификатор вашего мини-приложения.

Вы запустили своё первое мини-приложение внутри ВКонтакте. Заметьте, что мини-приложение будет работать, только пока оно и VK Tunnel запущены на вашем локальном компьютере. Чтобы мини-приложение работало автономно, вам потребуется разместить его на хостинге.

Если в браузере отображается ошибка Bad gateway, проверьте, что мини-приложение запущено, а если ошибка Error 1, — проверьте VK Tunnel.

Как поделиться мини-приложением с друзьями?

В конечном итоге вы получили ссылку на мини-приложение внутри ВКонтакте: vk.com/app51405499.

Размещение мини-приложения на хостинге

На предыдущем шаге вы запустили мини-приложение на своём локальном компьютере и получили ссылку на него внутри ВКонтакте. Но как только вы закроете окно терминала, мини-приложение прекратит работу.

Чтобы мини-приложение работало автономно, разместите его на хостинге. Мы создали библиотеку vk-miniapps-deploy, чтобы вы могли воспользоваться нашим хостингом. Также вы можете разместить мини-приложение в облаке VK Cloud.

1. Перейдите в каталог проекта:

    cd <MINI_APP_NAME>

2. Установите библиотеку vk-miniapps-deploy:

    npm install @vkontakte/vk-miniapps-deploy --include=dev

3. Откройте файл vk-hosting-config.json в каталоге проекта. В поле app_id замените 0 на идентификатор вашего мини-приложения, который вы получили при регистрации. Сохраните изменения.

    {
    "static_path": "build",
    "app_id": 51405499,
    "endpoints": {
    "mobile": "index.html",
    "mvk": "index.html",
    "web": "index.html"
    }
    }

4. Разверните мини-приложение:

    npm run deploy
    
    Перед деплоем автоматически выполнится команда npm run build, соберётся проект, а в каталоге проекта появится файл build.zip и каталог build.

5. Согласитесь на настройки по умолчанию: введите Y/y или нажмите Enter.
6. В командной строке вы получите ссылку вида: https://oauth.vk.com/code_auth?stage=check&code=1c2d2bd. Откройте её в браузере, чтобы пройти аутентификацию.
7. Вернитесь в терминал и подтвердите действие в командной строке: введите Y/y или нажмите Enter.
8. Подтвердите размещение мини-приложения на хостинге: введите код из личных сообщений от Администрации ВКонтакте. Также в push-уведомлении нужно подтвердить автоматическое изменение URL вашего мини-приложения.

    Если мини-приложение не размещается, проверьте, что в поле app_id указан корректный идентификатор вашего мини-приложения.

9. Перейдите по ссылке vk.com/app<id>, чтобы увидеть работу мини-приложения. Мини-приложение размещено на хостинге ВКонтакте, а ссылка вида: https://prod-app1-1.pages-ac.vk-apps.com/index.html появилась в поле URL в разделе Настройки.

Как поделиться мини-приложением с друзьями?

Ваше первое мини-приложение готово к использованию и дальнейшей разработке. Вы можете почитать документацию о функциональности мини-приложений в разделе Что дальше. А теперь коротко.

Краткая инструкция

1. Зарегистрируйте мини-приложение и получите его идентификатор.
2. Перейдите в папку, в которой хотите создать проект мини-приложения:

    cd <ПУТЬ_К_ПАПКЕ>

3. Создайте проект:

    npx @vkontakte/create-vk-mini-app

4. Перейдите в папку с проектом:

    cd mini-app

5. В файле vk-hosting-config.json в поле app_id замените 0 на идентификатор мини-приложения.
6. Установите библиотеку vk-miniapps-deploy:

    npm install @vkontakte/vk-miniapps-deploy --include=dev

7. Разверните мини-приложение:

    npm run deploy

8. Откройте ссылку vk.com/app<ID>.

Что дальше

Инструкции

• Если вам необходимо больше информации про первые шаги, посмотрите видеоурок: Часть 1. Первые шаги.

• Если вы готовы разрабатывать собственное приложение, посмотрите видеоурок: Часть 2. Лайвкодинг.

• Если вы ещё не работали с React, рекомендуем почитать официальное руководство.

• Если вы уже начали разработку, ознакомьтесь со списком рекомендаций для тех мини-приложений, которые мы размещаем в каталогах.

Библиотеки

• Библиотека VK Bridge необходима для взаимодействия с приложением ВКонтакте.

• Библиотека VKUI позволяет использовать компоненты интерфейса.

• Библиотека VK Icons содержит SVG-иконки на все случаи жизни.

Важно! Библиотеку VK Bridge необходимо использовать при разработке любого мини-приложения. Остальные библиотеки — не обязательно.

FAQ

Не удалось выполнить инструкцию, получаю ошибки. Что делать?

Убедитесь, что вы:

• установили необходимое программное обеспечение;

• используете Node.js 16.x.x.

Если всё равно возникают ошибки, поищите ответ в сообществе VK Mini Apps.

После выполнения команды создания проекта мини-приложения на Windows 10 Pro получаю ошибку. Что делать?

Если вы используете операционную систему Windows 10 Pro и после выполнения команды npx @vkontakte/create-vk-mini-app <MINI_APP_NAME> вы получили ошибку:

1. Перейдите в созданную папку проекта мини-приложения:

    cd <ПУТЬ_К_ПАПКЕ_MINI_APP_NAME>

2. Установите зависимости Node.js:

    npm install

3. Установите модули из файла package-lock.json:

    npm ci

После того как вы выполните эти команды, вы сможете продолжить выполнять инструкцию.

Получаю ошибку sh: 1: vk-tunnel: Permission denied. Что делать?

Если вы выполнили команду npm run tunnel на Linux и видите ошибку доступа, выдайте права на выполнение исполняемому файлу библиотеки:

chmod +x <ПОЛНЫЙ_ПУТЬ_ДО_ПРОЕКТА_МИНИ_ПРИЛОЖЕНИЯ>/node_modules/@vkontakte/vk-tunnel/bin/vk-tunnel

Получаю ошибку Error: 5: User authorization failed: invalid session. Что делать?

Если вы выполнили команду npm run deploy и видите ошибку авторизации, обновите токен библиотеки:

rm ~/.config/configstore/@vkontakte/vk-miniapps-deploy.json

Получаю ошибку Error: Пользователь не является создателем приложения. Что делать?

Если вы выполнили команду npm run tunnel и видите ошибку ERROR: Пользователь не является создателем приложения, обновите токен утилиты:

rm ~/.config/configstore/@vkontakte/vk-tunnel.json

Обратите внимание! Если ошибка сохраняется, убедитесь, что вас добавили в администраторы мини-приложения.

Получаю ошибку Error: connect ECONNREFUSED 127.0.0.1:10888. Что делать?

Убедитесь, что вы запустили проект:

npm start

Какие ещё приложения можно создать?

Попробуйте зарегистрировать:

• Встраиваемое приложение — вы получите идентификатор мини-приложения, которое можно встроить во фрейм с внешнего сайта. Готовые мини-приложения можно увидеть в наших каталогах: Мини-приложения, Игры.

• Standalone-приложение — вы получите идентификатор API_ID для внешнего сайта, мобильного или десктопного клиента. В интерфейсе такого приложения можно настроить SDK и подключить сертификаты для push-уведомлений.

• Сайт — вы получите идентификатор API_ID для внешнего сайта и работы с API через сервер. Если вы хотите написать скрипт (например, на PHP), который будет обращаться к API ВКонтакте, выберите именно этот вариант.

• Скилл Маруси — вы получите идентификатор приложения (скилла), которое взаимодействует с голосовым помощником и расширяет его базу навыков.

Как подключить стили CSS в мини-приложении?

Подключите стили в файле index.js:

import './style.css';

Если стили подключены неправильно, в мини-приложении отобразится пустая страница.

Как поделиться мини-приложением с друзьями?

По умолчанию мини-приложение видно только его создателю по ссылке vk.com/app<ID>.

Чтобы открыть мини-приложение всем, зайдите в Настройки. Измените Состояние мини-приложения на Приложение включено и видно всем.

Чтобы открыть мини-приложение конкретному пользователю, создайте группу тестировщиков в разделе Тестирование.

Внешний вид настроек изменения видимости мини-приложения
Изменение видимости мини-приложения
Внешний вид окна Создание группы тестировщиков
Создание группы тестировщиков

У меня есть постоянная ссылка на мини-приложение, но я хочу продолжить его разрабатывать. Как это сделать?

Чтобы продолжить разработку мини-приложения и иметь ссылку на него, переключитесь в режим разработки и запустите VK Tunnel.

Запустить мини-приложение внутри ВКонтакте.

Как сделать работу мини-приложения корректной на обоих доменах ВКонтакте — vk.com и vk.ru?

Поскольку некоторые разработчики валидируют входящие запросы и указывают в конфигурации мини-приложения адреса надёжных сайтов, не забудьте добавить домен vk.ru в white list. Это нужно, чтобы ваше мини-приложение работало корректно у пользователей, которые запустили его на домене vk.ru.

Если в своих мини-приложениях при отправке ответов с сервера вы используете заголовок X-Frame-Options, то рекомендуем внести правки, чтобы поддержать новые значения — vk.ru и m.vk.ru.

У меня возникли проблемы при разработке мини-приложения в режиме инкогнито

Из-за политик безопасности некоторые браузеры блокируют куки и localStorage в режиме инкогнито. Поэтому некоторые мини-приложения падают при обращении к localStorage через JavaScript. Используйте следующие методы VK Bridge вместо сохранения данных в localStorage:

• VKWebAppStorageSet

• VKWebAppStorageGetKeys

• VKWebAppStorageGet