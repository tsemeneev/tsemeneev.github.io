#### Техническое задание:
- при запуске бота, бот присылает приветствие и 3 кнопки:  ==Водитель==, ==Пассажир==, ==Связь с Администратором==

##### Линия водителя:
- При нажатии на кнопку ==Водитель==, бот проверяет id пользователя в базе данных `drivers`. 
- Если пользователя в базе нет, бот отправляет сообщение с кнопкой о необходимости пройти регистрацию, по нажатию на кнопку открывается форма регистрации с полями: Имя, Марка и модель машины, Фото машины, Номер телефона. Все поля обязательны к заполнению. После указания данных, пользователь жмёт кнопку зарегистрироваться и данные сохраняются в БД. После чего бот по новой проверяет id пользователя в БД.
- Если  пользователь найден в БД, бот предлагает ему создать поездку, и поочередно запрашивает данные: Откуда выезжаете (город + определенное место в городе), Дата и время выезда, Колличество свободных мест, В какой город поедете, Какие города будете проезжать.
- После указания всех пунктов, данные поездки сохраняются в отдельную БД со статусом ==неактивна== и списком пассажиров (который пока пустой), далее бот присылает пользователю данные поездки с кнопкой ==активировать==, для проверки, которые он может изменить. После проверки данных пользователь жмёт кнопку ==активировать==, и поездка становится активной для пассажиров.
- Водитель может просматривать свои поездки и редактировать их, если в поездке ещё нет пассажиров

##### Линия пассажира
- После нажатия на кнопку ==Пассажир==, бот отправляет запрос в БД users, если данных пользователя нет, бот отправляет запрос на сохранение данных с полями id, fullname, username 
###### Первый вариант:
Создаются чаты на каждый город России, и после сохранения данных пассажира в БД, ему будет предоставлена ссылка на его город. Также все заявки по этому городу будут публиковаться в этом чате
###### Второй вариант:
- После сохранения данных пассажира в БД, у пользователя появляется кнопка Найти поездку, по нажатию на которую пользователь поочередно отвечает на вопросы: Из какого города вы едете? => В какой город вы едете?
- После получения данных бот идёт в БД с поездками и ищет сначала прямые поездки, а после транзитные. Поездка будет отображаться с именем водителя, фото его машины, указанием пункта А и пункта Б, место и время встречи с водителем, количество свободных мест и кнопкой ==Поеду с {Имя водителя}==. 
- После нажатия на кнопку, бот присылает водителю этой поездки сообщение У вас новый пассажир @username. Напишите ему и согласуйте детали поездки.
- Также после нажатия бот добавляет пассажира в список пассажиров данной поездки. Когда количество пассажиров будет равно количеству свободных мест, статус поездки меняется на ==неактивна== и она не отображается.


#### Связь с Администратором
Бот предоставляет @username Администратора для дальнейшего обсуждения вопроса
