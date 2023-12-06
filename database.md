## диаграмма
![awwawa](https://github.com/ishouldbefound/SQL/assets/144837901/e5d247ce-c488-4d32-b02b-059dda6f6c81)
## Создание таблиц
```sql
CREATE TABLE Countries (
  id INT PRIMARY KEY,
  Country VARCHAR(255) NOT NULL
);

CREATE TABLE Guests (
  id INT PRIMARY KEY,
  Firstname VARCHAR(255) NOT NULL,
  Surname VARCHAR(255) NOT NULL,
  Phone_number VARCHAR(15),
  email VARCHAR(255),
  Birthday DATE,
  Sex VARCHAR(10),
  Country_id INT,
  last_modified TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (Country_id) REFERENCES Countries(id)
);

CREATE TABLE Services (
  id INT PRIMARY KEY,
  title VARCHAR(255) NOT NULL,
  description TEXT,
  price FLOAT NOT NULL,
  Phone_number VARCHAR(15)
);

CREATE TABLE Services_orders (
  id INT PRIMARY KEY,
  price FLOAT NOT NULL,
	service_id INT NOT NULL,
	guest_id INT NOT NULL,
	FOREIGN KEY (service_id) REFERENCES Services(id),
  FOREIGN KEY (guest_id) REFERENCES Guests(id)
);

CREATE TABLE Payments (
  id INT PRIMARY KEY,
	guest_id INT NOT NULL,
  description VARCHAR(255) NOT NULL,
  order_date DATE NOT NULL,
  price FLOAT NOT NULL,
  FOREIGN KEY (guest_id) REFERENCES Guests(id)
);

CREATE TABLE Room_types (
  id INT PRIMARY KEY,
  type VARCHAR(255),
  description VARCHAR(255)
);

CREATE TABLE Statuses (
  id INT PRIMARY KEY,
  status VARCHAR(255)
);

CREATE TABLE Rooms (
  id INT PRIMARY KEY,
  type_id INT NOT NULL,
  status_id INT NOT NULL,
  price FLOAT NOT NULL,
  FOREIGN KEY (type_id) REFERENCES Room_types(id),
  FOREIGN KEY (status_id) REFERENCES Statuses(id)
);

CREATE TABLE Bonuses (
  id INT PRIMARY KEY,
  description VARCHAR(255) NOT NULL
);

CREATE TABLE Guest_loyalty (
  id INT PRIMARY KEY,
  guest_id INT,
  status_id INT,
  bonus_id INT,
  FOREIGN KEY (guest_id) REFERENCES Guests(id),
  FOREIGN KEY (status_id) REFERENCES Statuses(id),
  FOREIGN KEY (bonus_id) REFERENCES Bonuses(id)
);

CREATE TABLE Review (
  id INT PRIMARY KEY,
  guest_id INT,
  service_id INT,
  rating INT,
  comment VARCHAR(255),
  FOREIGN KEY (guest_id) REFERENCES Guests(id),
  FOREIGN KEY (service_id) REFERENCES Services(id)
);

CREATE TABLE Bookings (
  id INT PRIMARY KEY,
  guest_id INT,
  room_id INT,
  arrival_date DATE,
  departure_date DATE,
  total_cost FLOAT,
  FOREIGN KEY (guest_id) REFERENCES Guests(id),
  FOREIGN KEY (room_id) REFERENCES Rooms(id)
);

CREATE TABLE Departments (
  id INT PRIMARY KEY,
  title VARCHAR(255),
  description TEXT
);

CREATE TABLE Staff_positions (
  id INT PRIMARY KEY,
  position VARCHAR(255),
  description TEXT
);

CREATE TABLE Staff (
  id INT PRIMARY KEY,
  name VARCHAR(255),
  surname VARCHAR(255),
  position_id INT,
  phone_number VARCHAR(20),
  FOREIGN KEY (position_id) REFERENCES Staff_positions(id)
);

CREATE TABLE Staff_departments (
  id INT PRIMARY KEY,
  department_id INT,
  staff_id INT,
  FOREIGN KEY (staff_id) REFERENCES Staff(id)
);
```

## Внесение записей в таблицу
```sql
INSERT INTO Countries (id, Country) VALUES
  (1, 'США'),
  (2, 'Канада'),
  (3, 'Бразилия'),
  (4, 'Франция'),
  (5, 'Германия'),
  (6, 'Индия'),
  (7, 'Китай'),
  (8, 'Япония'),
  (9, 'Австралия'),
  (10, 'Мексика'),
  (11, 'Аргентина'),
  (12, 'Россия'),
  (13, 'Южная Африка'),
  (14, 'Италия'),
  (15, 'Испания'),
  (16, 'Великобритания'),
  (17, 'Нидерланды'),
  (18, 'Швейцария'),
  (19, 'Швеция'),
  (20, 'Норвегия'),
  (21, 'Новая Зеландия'),
  (22, 'Южная Корея'),
  (23, 'Сингапур'),
  (24, 'Таиланд'),
  (25, 'Египет'),
  (26, 'Нигерия'),
  (27, 'Саудовская Аравия'),
  (28, 'Турция'),
  (29, 'Вьетнам'),
  (30, 'Чили');

INSERT INTO Guests (id, Firstname, Surname, Phone_number, email, Birthday, Sex, Country_id)
VALUES
  (1, 'Иван', 'Иванов', '123456789', 'ivan@example.com', '1990-01-15', 'Мужской', 3),
  (2, 'Елена', 'Петрова', '987654321', 'elena@example.com', '1985-05-22', 'Женский', 15),
  (3, 'Алексей', 'Сидоров', '555111333', 'alex@example.com', '1988-09-10', 'Мужской', 8),
  (4, 'Мария', 'Кузнецова', '777888999', 'maria@example.com', '1995-03-03', 'Женский', 12),
  (5, 'Дмитрий', 'Смирнов', '111222333', 'dmitry@example.com', '1982-07-18', 'Мужской', 5),
  (6, 'Ольга', 'Иванова', '444555666', 'olga@example.com', '1993-12-01', 'Женский', 19),
  (7, 'Андрей', 'Павлов', '666777888', 'andrew@example.com', '1987-11-25', 'Мужской', 26),
  (8, 'Наталья', 'Морозова', '222333444', 'natalia@example.com', '1991-08-07', 'Женский', 13),
  (9, 'Сергей', 'Федоров', '999000111', 'sergey@example.com', '1984-04-14', 'Мужской', 7),
  (10, 'Анна', 'Николаева', '123123456', 'anna@example.com', '1998-06-30', 'Женский', 2),
  (11, 'Павел', 'Григорьев', '456789012', 'pavel@example.com', '1989-02-28', 'Мужской', 11),
  (12, 'Екатерина', 'Васильева', '789012345', 'ekaterina@example.com', '1996-10-05', 'Женский', 21),
  (13, 'Игорь', 'Андреев', '234567890', 'igor@example.com', '1983-09-20', 'Мужской', 28),
  (14, 'Юлия', 'Степанова', '567890123', 'yulia@example.com', '1994-04-02', 'Женский', 9),
  (15, 'Максим', 'Козлов', '890123456', 'maxim@example.com', '1986-12-15', 'Мужской', 17),
  (16, 'Виктория', 'Орлова', '345678901', 'viktoria@example.com', '1997-07-08', 'Женский', 4),
  (17, 'Артем', 'Тимофеев', '678901234', 'artem@example.com', '1981-01-11', 'Мужской', 23),
  (18, 'Евгения', 'Гущина', '012345678', 'evgenia@example.com', '1992-05-26', 'Женский', 14),
  (19, 'Денис', 'Белов', '901234567', 'denis@example.com', '1980-08-24', 'Мужской', 10),
  (20, 'Маргарита', 'Макарова', '456789012', 'margarita@example.com', '1999-11-17', 'Женский', 27),
  (21, 'Никита', 'Захаров', '123456789', 'nikita@example.com', '1985-03-30', 'Мужской', 6),
  (22, 'Татьяна', 'Борисова', '789012345', 'tatyana@example.com', '1993-09-05', 'Женский', 18),
  (23, 'Григорий', 'Кудряшов', '234567890', 'grigory@example.com', '1987-06-12', 'Мужской', 22),
  (24, 'Анастасия', 'Антонова', '567890123', 'anastasia@example.com', '1990-02-22', 'Женский', 1),
  (25, 'Роман', 'Герасимов', '890123456', 'roman@example.com', '1984-10-15', 'Мужской', 25),
  (26, 'Елена', 'Волкова', '012345678', 'elena@example.com', '1996-07-28', 'Женский', 16),
  (27, 'Александр', 'Соколов', '901234567', 'alexander@example.com', '1982-12-03', 'Мужской', 20),
  (28, 'Марина', 'Фролова', '345678901', 'marina@example.com', '1998-04-18', 'Женский', 29),
  (29, 'Илья', 'Комаров', '678901234', 'ilya@example.com', '1989-11-07', 'Мужской', 24),
  (30, 'Оксана', 'Полякова', '123456789', 'oksana@example.com', '1991-06-23', 'Женский', 30);

INSERT INTO Services (id, title, description, price, Phone_number)
VALUES
  (1, 'Проживание в стандартном номере', 'Уютный номер с основными удобствами', 100.00, '123456789'),
  (2, 'Проживание в люксе', 'Просторный номер с шикарным видом', 200.00, '987654321'),
  (3, 'Завтрак "Шведский стол"', 'Обилие разнообразных блюд на завтрак', 15.00, '555111333'),
  (4, 'Ужин в ресторане', 'Пятиблюдное меню от шеф-повара', 50.00, '777888999'),
  (5, 'Спа-процедуры', 'Расслабление и оздоровление в нашем спа', 80.00, '111222333'),
  (6, 'Экскурсии по окрестностям', 'Увлекательные поездки с опытным гидом', 30.00, '444555666'),
  (7, 'Бассейн с подогревом', 'Круглогодичное плавание в комфортной воде', 25.00, '666777888'),
  (8, 'Конференц-зал аренда', 'Просторное помещение для деловых мероприятий', 150.00, '222333444'),
  (9, 'Услуги прачечной', 'Стирка и глажка вашей одежды', 10.00, '999000111'),
  (10, 'Бесплатный Wi-Fi', 'Быстрый и надежный интернет в номере и на территории', 0.00, '123123456');

INSERT INTO Services_orders (id, price, service_id, guest_id)
VALUES
  (1, 100.00, 7, 1),
  (2, 200.00, 3, 6),
  (3, 15.00, 8, 21),
  (4, 50.00, 4, 23),
  (5, 80.00, 3, 7),
  (6, 30.00, 5, 11),
  (7, 25.00, 7, 16),
  (8, 150.00, 8, 30),
  (9, 10.00, 9, 13),
  (10, 0.00, 10, 9),
  (11, 40.00, 5, 17),
  (12, 20.00, 4, 22),
  (13, 5.00, 6, 3),
  (14, 30.00, 6, 8),
  (15, 60.00, 2, 15),
  (16, 100.00, 8, 16),
  (17, 10.00, 2, 17),
  (18, 8.00, 1, 18),
  (19, 12.00, 5, 29),
  (20, 5.00, 9, 18),
  (21, 15.00, 4, 21),
  (22, 18.00, 3, 24),
  (23, 5.00, 7, 16),
  (24, 12.00, 2, 19),
  (25, 200.00, 7, 25),
  (26, 250.00, 9, 4),
  (27, 30.00, 2, 3),
  (28, 10.00, 6, 7),
  (29, 15.00, 5, 4),
  (30, 80.00, 4, 14);

INSERT INTO Room_types (id, type, description)
VALUES
  (1, 'Стандартный номер', 'Просторный номер с удобствами для комфортного проживания.'),
  (2, 'Люкс', 'Элегантный номер с отдельной спальней и гостиной зоной.'),
  (3, 'Фэмили номер', 'Просторный номер с несколькими кроватями, идеальный для семей.'),
  (4, 'Сьют', 'Роскошный номер с отдельной спальней, гостиной и кухонной зоной.'),
  (5, 'Эконом номер', 'Уютный номер с минимальным набором удобств по доступной цене.');

INSERT INTO Statuses (id, status)
VALUES
  (1, 'Свободна'),
  (2, 'Занята'),
  (3, 'Действителен'),
  (4, 'Не действителен');

INSERT INTO Rooms (id, type_id, status_id, price)
VALUES
  (1, 1, 1, 1500.00),
  (2, 2, 1, 3000.00),
  (3, 3, 1, 2000.00),
  (4, 4, 2, 4000.00),
  (5, 5, 2, 1000.00),
  (6, 1, 1, 1600.00),
  (7, 2, 2, 3500.00),
  (8, 3, 1, 2200.00),
  (9, 4, 1, 3800.00),
  (10, 5, 2, 1200.00),
  (11, 1, 2, 1700.00),
  (12, 2, 1, 3100.00),
  (13, 3, 2, 2300.00),
  (14, 4, 1, 4200.00),
  (15, 5, 1, 1100.00),
  (16, 1, 2, 1800.00),
  (17, 2, 1, 3200.00),
  (18, 3, 2, 2500.00),
  (19, 4, 1, 4000.00),
  (20, 5, 2, 1300.00),
  (21, 1, 1, 1400.00),
  (22, 2, 2, 3300.00),
  (23, 3, 1, 2100.00),
  (24, 4, 1, 3600.00),
  (25, 5, 2, 900.00),
  (26, 1, 1, 1900.00),
  (27, 2, 2, 3700.00),
  (28, 3, 1, 2400.00),
  (29, 4, 1, 4100.00),
  (30, 5, 2, 1100.00);

INSERT INTO Bonuses (id, description)
VALUES
  (1, 'Бесплатный завтрак'),
  (2, 'Скидка на следующее бронирование'),
  (3, 'Дополнительный час в спа-центре'),
  (4, 'Бесплатная парковка'),
  (5, 'Подарок в номере'),
  (6, 'Бесплатный трансфер до аэропорта'),
  (7, 'Специальное угощение от ресторана'),
  (8, 'Бесплатный бассейн'),
  (9, 'Скидка на услуги ресторана'),
  (10, 'Бесплатный Wi-Fi в номере');

INSERT INTO Guest_loyalty (id, guest_id, status_id, bonus_id)
VALUES
  (1, 6, 3, 4),
  (2, 22, 4, 4),
  (3, 30, 3, 2),
  (4, 15, 4, 1),
  (5, 7, 3, 5),
  (6, 19, 4, 6),
  (7, 3, 3, 9),
  (8, 8, 4, 5),
  (9, 17, 3, 9),
  (10, 11, 4, 10);

INSERT INTO Review (id, guest_id, service_id, rating, comment)
VALUES
  (1, 5, 1, 5, 'Отличный сервис, прекрасный персонал!'),
  (2, 2, 2, 4, 'Хорошие услуги, но небольшие недочеты.'),
  (3, 7, 3, 5, 'Превосходный отдых, все было замечательно!'),
  (4, 25, 4, 3, 'Неплохо, но есть место для улучшений.'),
  (5, 15, 5, 5, 'Отличное обслуживание, с удовольствием вернусь!'),
  (6, 30, 1, 4, 'Сервис на высоте, но цены чуть выше среднего.'),
  (7, 12, 2, 5, 'Услуги полностью соответствуют ожиданиям!'),
  (8, 5, 3, 3, 'Не все понравилось, есть небольшие замечания.'),
  (9, 6, 4, 5, 'Великолепный отдых, все понравилось без исключения!'),
  (10, 12, 5, 4, 'Хорошее обслуживание, но немного шумно в номере.'),
  (11, 11, 1, 5, 'Превосходный сервис, отличное отношение персонала!'),
  (12, 14, 2, 4, 'Удобные услуги, но немного нехватка внимания.'),
  (13, 16, 3, 5, 'Отдых был на высшем уровне, все понравилось!'),
  (14, 17, 4, 3, 'Средний уровень, есть небольшие недоработки.'),
  (15, 19, 5, 5, 'Прекрасное обслуживание, обязательно приду снова!'),
  (16, 18, 1, 4, 'Хороший сервис, но немного дорого.'),
  (17, 24, 2, 5, 'Услуги на высшем уровне, все отлично!'),
  (18, 23, 3, 3, 'Есть некоторые замечания по услугам.'),
  (19, 21, 4, 5, 'Отдых прошел замечательно, все понравилось!'),
  (20, 20, 5, 4, 'Хорошее обслуживание, немного шумно в номере.');

INSERT INTO Bookings (id, guest_id, room_id, arrival_date, departure_date, total_cost)
VALUES
  (1, 1, 1, '2023-01-15', '2023-01-20', 500),
  (2, 2, 2, '2023-01-15', '2023-01-20', 500),
  (3, 3, 3, '2023-01-15', '2023-01-20', 500),
  (4, 4, 4, '2023-01-15', '2023-01-20', 500),
  (5, 5, 5, '2023-01-15', '2023-01-20', 500),
  (6, 6, 6, '2023-01-15', '2023-01-20', 500),
  (7, 7, 7, '2023-01-15', '2023-01-20', 500),
  (8, 8, 8, '2023-01-15', '2023-01-20', 500),
  (9, 9, 9, '2023-01-15', '2023-01-20', 500),
  (10, 10, 10, '2023-01-15', '2023-01-20', 500),
  (11, 11, 11, '2023-01-15', '2023-01-20', 500),
  (12, 12, 12, '2023-01-15', '2023-01-20', 500),
  (13, 13, 13, '2023-01-15', '2023-01-20', 500),
  (14, 14, 14, '2023-01-15', '2023-01-20', 500),
  (15, 15, 15, '2023-01-15', '2023-01-20', 500),
  (16, 16, 16, '2023-01-15', '2023-01-20', 500),
  (17, 17, 17, '2023-01-15', '2023-01-20', 500),
  (18, 18, 18, '2023-01-15', '2023-01-20', 500),
  (19, 19, 19, '2023-01-15', '2023-01-20', 500),
  (20, 20, 20, '2023-01-15', '2023-01-20', 500),
  (21, 21, 21, '2023-01-15', '2023-01-20', 500),
  (22, 22, 22, '2023-01-15', '2023-01-20', 500),
  (23, 23, 23, '2023-01-15', '2023-01-20', 500),
  (24, 24, 24, '2023-01-15', '2023-01-20', 500),
  (25, 25, 25, '2023-01-15', '2023-01-20', 500),
  (26, 26, 26, '2023-01-15', '2023-01-20', 500),
  (27, 27, 27, '2023-01-15', '2023-01-20', 500),
  (28, 28, 28, '2023-01-15', '2023-01-20', 500),
  (29, 29, 29, '2023-01-15', '2023-01-20', 500),
  (30, 30, 30, '2023-01-15', '2023-01-20', 500);

INSERT INTO Departments (id, title, description)
VALUES
  (1, 'Отдел ресепшн', 'Отдел занимается регистрацией гостей и предоставлением информации о гостинице.'),
  (2, 'Отдел обслуживания номеров', 'Отдел отвечает за поддержание чистоты в номерах и удовлетворение потребностей гостей.'),
  (3, 'Отдел кулинарии', 'Отдел приготовления блюд для ресторана гостиницы и обеспечение питания для гостей.'),
  (4, 'Отдел маркетинга', 'Отдел занимается продвижением гостиничных услуг и привлечением клиентов.'),
  (5, 'Отдел безопасности', 'Отдел обеспечивает безопасность гостей и соблюдение правил в гостинице.'),
  (6, 'Отдел конференций и мероприятий', 'Отдел организует конференции и мероприятия для гостей и компаний.'),
  (7, 'Отдел спа и велнеса', 'Отдел предоставляет услуги спа и велнеса для гостей, обеспечивая релаксацию и заботу о здоровье.'),
  (8, 'Отдел технической поддержки', 'Отдел обеспечивает техническую работоспособность оборудования в гостинице.'),
  (9, 'Отдел бухгалтерии', 'Отдел отвечает за учет финансовых операций и финансовое планирование гостиницы.'),
  (10, 'Отдел кадров', 'Отдел занимается подбором персонала, управлением кадровыми вопросами и обучением сотрудников.');

INSERT INTO Staff_positions (id, position, description)
VALUES
  (1, 'Администратор ресепшн', 'Отвечает за прием гостей, регистрацию, и предоставление информации о гостинице.'),
  (2, 'Горничная', 'Отвечает за уборку номеров и обеспечение чистоты в гостинице.'),
  (3, 'Повар', 'Отвечает за приготовление блюд в ресторане гостиницы.'),
  (4, 'Маркетолог', 'Занимается разработкой маркетинговых стратегий и продвижением услуг гостиницы.'),
  (5, 'Охранник', 'Отвечает за обеспечение безопасности гостей и имущества.'),
  (6, 'Координатор мероприятий', 'Занимается организацией и координацией конференций и мероприятий.'),
  (7, 'Специалист по спа-услугам', 'Предоставляет услуги спа и велнеса для гостей.'),
  (8, 'Инженер по обслуживанию техники', 'Отвечает за техническую работоспособность оборудования в гостинице.'),
  (9, 'Бухгалтер', 'Отвечает за ведение финансового учета и отчетности гостиницы.'),
  (10, 'Специалист по кадрам', 'Занимается подбором персонала, управлением кадровыми вопросами и обучением сотрудников.');

INSERT INTO Staff (id, name, surname, position_id, phone_number)
VALUES
  (1, 'Иван', 'Иванов', 1, '+7-999-123-45-67'),
  (2, 'Петр', 'Петров', 2, '+7-999-234-56-78'),
  (3, 'Мария', 'Сидорова', 3, '+7-999-345-67-89'),
  (4, 'Елена', 'Козлова', 4, '+7-999-456-78-90'),
  (5, 'Алексей', 'Смирнов', 5, '+7-999-567-89-01'),
  (6, 'Ольга', 'Иванова', 6, '+7-999-678-90-12'),
  (7, 'Дмитрий', 'Петров', 7, '+7-999-789-01-23'),
  (8, 'Наталья', 'Сидорова', 8, '+7-999-890-12-34'),
  (9, 'Сергей', 'Козлов', 9, '+7-999-901-23-45'),
  (10, 'Анна', 'Смирнова', 10, '+7-999-012-34-56');

INSERT INTO Staff_departments (id, department_id, staff_id)
VALUES
  (1, 1, 1),
  (2, 2, 2),
  (3, 3, 3),
  (4, 4, 4),
  (5, 5, 5),
  (6, 6, 6),
  (7, 7, 7),
  (8, 8, 8),
  (9, 9, 9),
  (10, 10, 10);
```

## Триггеры:
```sql
-- обновляет статус комнаты если до этого была свободна, а затем забронирована
CREATE OR REPLACE FUNCTION update_room_status()
RETURNS TRIGGER AS $$
BEGIN
  UPDATE Rooms
  SET status_id = 2
  WHERE id = NEW.room_id;

  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER bookings_update_room_status
AFTER INSERT ON Bookings
FOR EACH ROW
EXECUTE FUNCTION update_room_status();

-- обновляет статус комнаты после завершения бронирования
CREATE OR REPLACE FUNCTION update_room_status_after_checkout()
RETURNS TRIGGER AS $$
BEGIN
  IF NEW.departure_date IS NOT NULL THEN
    UPDATE Rooms
    SET status_id = 1
    WHERE id = NEW.room_id;
  END IF;

  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER bookings_update_room_status_after_checkout
BEFORE UPDATE ON Bookings
FOR EACH ROW
EXECUTE FUNCTION update_room_status_after_checkout();

-- создает новые записи в таблице Payments при вставке нового бронирования:
CREATE OR REPLACE FUNCTION create_payment_after_booking()
RETURNS TRIGGER AS $$
BEGIN
  INSERT INTO Payments (id, guest_id, description, order_date, price)
  VALUES (NEW.id, NEW.guest_id, 'Booking payment', NOW(), NEW.total_cost);

  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER bookings_create_payment
AFTER INSERT ON Bookings
FOR EACH ROW
EXECUTE FUNCTION create_payment_after_booking();
```