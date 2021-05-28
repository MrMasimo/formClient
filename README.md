# Форма регистрация нового клиента

Валидация проверятся с использованием Vuelidate.
Поля со * должны быть обязательно заполнены, все остальные по желанию.

Для полей _Фамилия, Имя, Дата рождения, Телефон, Индекс, Страна, Город, Дом, Дата выдачи документа_ созданы регулярные выражения.

При нажатии _Регистрация клиента_ происходит проверка валидации полей, и отображается сообщение об успешной или неуспешной регистрации клиента. После 2х секунд сообщение исчезает.