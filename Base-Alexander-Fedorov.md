# Чек-лист
## Команада Base, Александр Федоров
### Проект [Reazon](https://reazon.ru)

Тестируемые разделы:
1. [Страница профиля](https://github.com/thelvv/homework-3-spring-2023/blob/main/Base-Alexander-Fedorov.md#c%D1%82%D1%80%D0%B0%D0%BD%D0%B8%D1%86%D0%B0-%D0%BF%D1%80%D0%BE%D1%84%D0%B8%D0%BB%D1%8F)

# [Cтраница профиля](https://www.reazon.ru/user)
Креды для авторизации: test@test.test 123456

### Поведение для авторизованного и не авторизованного пользователя
1. При загрузке страницы без авторизации появляется строка "Войдите, чтобы посмотреть ваш профиль"
2. При загрузке страницы с авторизацией появляются блок личной информации, содержащий строки "Имя", "Почта", "Телефон", а также блоки банковских карт и адресов доставки

### Общие паттерны
1. Кнопка "Отменить" закрывает модальное окно, открывшееся:
   1. При попытке изменить поле в блоке личной информации нажатием на иконку карандаша напротив соответствующего поля
   2. При попытке изменить пароль нажатием на кнопку "Изменить пароль"
   3. При попытке добавить карту оплаты/адреса нажатием на карту с иконкой плюс
   4. При попытке изменить карточку адреса нажатием на иконку карандаша поверх данной карточки

   Изменения, введенные в поля модального окна, не сохраняются  
   Пример модального окна:  
   ![image](https://user-images.githubusercontent.com/59176894/235500296-852fb39e-cecc-4f67-8946-9ad18e4d9fe8.png)  
2. Под изменением поля/сущности понимается ввод в модальное окно тестовых данных и нажатие кнопки "Применить"
3. Название вкладки: "Ваши данные - Reazon"

### Блок аватарки
1. URL для исходной аватарки равен дефолтному - "https://www.reazon.ru/img/UserPhoto.webp"
2. При изменении аватарки (клик по карандашу поверх картинки) ее путь не равен исходному
3. После перезагрузки путь аватарки все еще не равен исходному

### Блок имени
1. При изменении имени на непустую строку изменение происходит, в поле "Имя" отображается строка, переданная в тесте
2. При изменении имени на пустую строку появляется сообщение об ошибке "Поле обязательно должно быть заполнено"

### Блок почты
1. При изменении почты на корректную (regex: @) изменение происходит, в поле "Почта" отображается строка, переданная в тесте
2. При изменении почты на некорректную появляется сообщение об ошибке
   1. При вводе пустой строки появляется сообщение об ошибке "Поле обязательно должно быть заполнено"
   2. При вводе строки, несоответсвующей regex: @, появляется сообщение об ошибке "Неверный формат почты"

### Блок номера телефона
1. При изменении номера телефона на корректный (11 цифр, начинается с +7) изменение происходит, в поле "Телефон" отображается строка, переданная в тесте
2. При изменении номера телефона на некорректный появляется сообщение об ошибке
   1. При вводе пустой строки появляется сообщение об ошибке "Поле обязательно должно быть заполнено"
   2. При вводе номера не из 11 символов появляется сообщение об ошибке "Телефон должен содержать 11 цифр. Введено __N__/11"

### Блок изменения пароля
1. При изменении пароля и выполнения всех условий (правильность текущего пароля, >=6 символов в новом и совпадение новых) изменение происходит, возвращается статус 200
2. При неправильных данных появляется сообщение об ошибке
   1. При незаполнении хотя бы одного из полей "Старый пароль" и "Новый пароль" появляется сообщение об ошибке "Поле обязательно должно быть заполнено" напротив данного поля
   2. При вводе нового пароля длиной <6 символов появляется сообщение об ошибке "Пароль должен содержать минимум 6 символов"
   3. При вводе разных строк в инпуты нового пароля появляется сообщение об ошибке "Введенные пароли не совпадают"
   4. При вводе текущего пароля длиной <6 символов и нового пароля длиной >=6 символов появляется сообщение об ошибке "Пароль должен содержать минимум 6 символов"
   5. При вводе неверного текущего пароля появляется сообщение об ошибке "Старый пароль не верный"

### Блок банковских карт
1. При корреткном заполнении полей модального окна добавления карты - она добавляется, возвращается статус 200
2. При некорректном заполнении полей добавления карты появляется ошибка
   1. При некорректном заполнении (строкой, содержащей не 16 цифр) поля номера карты появляется ошибка "Номер карты состоит из 16 цифр. __N__/16"
   2. При незаполнении полей даты окончания обслуживания карты появляется ошибка "Срок действия карты формата 09/25"
   3. При заполнении полей даты окончания обслуживания карты прошедшей датой появляется ошибка "Срок действия карты истек"
   4. При заполнении поля месяца даты окончания обслуживания карты числом, большим 12, появляется ошибка "Месяц не может быть больше 12"
   5. При некорректном (строкой, содержащей не 3 цифры) заполнении поля CVV-кода появляется ошибка "CVC код содержит 3 цифры"
3. При добавлении 4 карт кнопка добавления новой пропадает
4. При клике на иконку корзины поверх данной карты происходит ее удаление, возвращается статус 200

### Блок карточек адреса
1. Работает добавление новой карты без указания квартиры, возвращается статус 200
2. Работает добавление новой карты с указанием квартиры, возвращается статус 200
3. При вводе пустой строки в поля:
   1. Города - появляется ошибка "Введите ваш город"
   2. Улицы - появляется ошибка "Введите вашу улицу"
   3. Дома - появляется ошибка "Введите ваш дом"
5. При добавлении 4 карт кнопка добавления новой пропадает
6. При клике на иконку корзины поверх данной карточки происходит ее удаление, возвращается статус 200
7. При вводе непустых строк в поля города, улицы и дома при изменении адреса происходит его изменение, возвращается статус 200
