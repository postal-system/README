# Postal system (Почтовая система)

![This is an image](Postal-system-General.drawio.png)<br/>

Почтовая система построена на основе микросервисной архитектуры, она
состоит из 10 микросервисов и стартера. <br/>

Система принимает письма и посылки в виде JSON-сообщений по общей шине,
а затем обрабатывает их и регистрирует в базе данных для дальнейшего ведения
статистики и формирования отчетов.<br/>

Отчеты формируются по заданным фильтрам, результат сохраняется в виде
файла в формате PDF, XML, XLSX, CSV. <br/>

Почтовая система интегрирована с внешней системой - ”Личным кабинетом
“Энергосбытовая компания" (ESK), из которой она получает входящую информацию
(письма, посылки), а также подтягивает дополнительную информацию для сервисов
Почтовой системы. <br/>

Система использует СУБД PostgreSQL в качестве основной, взаимодействие с
базой осуществляется при помощи технологии Spring JPA. <br/>

Микросервисы взаимодействуют используя REST-запросы и общую шину на
базе Kafka (при этом есть возможность использовать вместо нее RabbitMQ). <br/>

Тестирование производится в контейнерах, что позволяет тестировать
приложения локально пользуясь всеми преимуществами полноценной базы и шины. 

## ИСПОЛЬЗУЕМЫЕ ТЕХНОЛОГИИ 

- Apache Maven
- Java 11, Kotlin
- Spring Boot: core, web, test, data-jpa
- Apache Kafka, RabbitMQ
- Spring-Cloud: OpenFeign
- Testcontainers
- Swagger UI
- Mapstuct
- Jackson
- Lombok
- Checkstyle,  Detekt
- PostgreSQL
- Docker
- Nexus

## ИНТЕГРАЦИЯ С ВНЕШНЕЙ СИСТЕМОЙ
Проведена интеграция с системой “Личный кабинет “Энергосбытовая компания”
(ESK), параллельно разрабатываемой другой группой стажеров-разработчиков.
Почтовая система интегрируется с 3 микросервисами ESK:
1. Order service (ESK), отправляет в шину письмо, которое далее обрабатывается
   сервисом Shipment Receiver
2. User service (ESK), предоставляет данные о получателе для сервиса Shipment
   Receiver
3. Post Office service (PEJT) предоставляет для ESK список почтовых отделений по
   заданному фильтру