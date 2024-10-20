# CRM-система

## Описание проекта

CRM-система (Customer Relationship Management) предназначена для управления информацией о продавцах и их транзакциях. Система позволяет выполнять основные операции CRUD (создание, чтение, обновление и удаление) для продавцов и транзакций, а также предоставляет аналитические функции для анализа эффективности продавцов.

## Функциональность


### Управление продавцами
- **Создание нового продавца**
- **Получение информации о продавце по ID**
- **Обновление информации о продавце**
- **Удаление продавца**
- **Получение списка всех продавцов**

#### Аналитика
- **Получение самого продуктивного продавца за указанный период**
- **Получение списка продавцов с суммой транзакций ниже указанного порога за указанный период**
- **Получение самого продуктивного времени продавца**

### Управление транзакциями
- **Создание новой транзакции**
- **Получение информации о транзакции по ID**
- **Обновление информации о транзакции**
- **Удаление транзакции**
- **Получение всех транзакций**
- **Получение всех транзакций по ID продавца**

## Инструкции по сборке и запуску

### Требования
- Java 21
- Docker

### Сборка и запуск проекта

Запуск БД в Docker Compose
```bash
docker-compose up -d
```
Запуск Spring Boot приложения
```bash
./gradlew clean bootRun
```
или в IntelliJ Idea 😀


## Примеры использования API

### Управление продавцами

1. **Получить список всех продавцов**
    - **GET** `http://localhost:8080/seller`


2. **Получить информацию о конкретном продавце**
    - **GET** `http://localhost:8080/seller/{id}`
    - **Пример**: `http://localhost:8080/seller/9`


3. **Создать нового продавца**
    - **POST** `http://localhost:8080/seller`
    - **Content-Type**: `application/json`
    - **Тело запроса**:
      ```json
      {
        "id": 50,
        "name": "Сергей Сергеев",
        "contactInfo": "ivan@example.com",
        "registrationDate": "2024-10-19T13:20:31"
      }
      ```

4. **Обновить информацию о продавце**
    - **PUT** `http://localhost:8080/seller/{id}`
    - **Пример**: `http://localhost:8080/seller/2`
    - **Content-Type**: `application/json`
    - **Тело запроса**:
      ```json
      {
        "name": "Юрий Иванов"
      }
      ```

5. **Удалить продавца**
    - **DELETE** `http://localhost:8080/seller/{id}`
    - **Пример**: `http://localhost:8080/seller/21`


#### Аналитика


6. **Получение самого продуктивного продавца за указанный период**
    - **GET** `http://localhost:8080/seller/transactions/most-productive?startDate={startDate}&endDate={endDate}`
    - **Пример**: `http://localhost:8080/seller/transactions/most-productive?startDate=2023-01-01T00:00:00&endDate=2024-10-20T23:59:59`


7. **Получить список продавцов с суммой транзакций ниже указанного порога за указанный период**
    - **GET** `http://localhost:8080/seller/transactions/less-than?startDate={startDate}&endDate={endDate}&threshold={threshold}`
    - **Пример**: `http://localhost:8080/seller/transactions/less-than?startDate=2023-01-01T00:00:00&endDate=2024-10-20T23:59:59&threshold=1000`


8. **Получить самое продуктивное время продавца**
    - **GET** `http://localhost:8080/seller/{sellerId}/productive-period`
    - **Пример**: `http://localhost:8080/seller/2/most-productive-time?startDate=2022-01-01T00:00:00&endDate=2024-10-20T23:59:59`

---

### Управление транзакциями

1. **Получить список всех транзакций**
    - **GET** `http://localhost:8080/transaction`


2. **Получить информацию о конкретной транзакции**
    - **GET** `http://localhost:8080/transaction/{id}`
    - **Пример**: `http://localhost:8080/transaction/50`


3. **Получить все транзакции продавца**
    - **GET** `http://localhost:8080/transaction/seller/{sellerId}`
    - **Пример**: `http://localhost:8080/transaction/seller/2`


4. **Создать новую транзакцию для указанного продавца**
    - **POST** `http://localhost:8080/transaction/seller/{sellerId}`
    - **Пример**: `http://localhost:8080/transaction/seller/2`
    - **Content-Type**: `application/json`
    - **Тело запроса**:
      ```json
      {
        "amount": 10000,
        "paymentType": "CASH",
        "transactionDate": "2023-02-02T15:30:00"
      }
      ```


5. **Обновить существующую транзакцию по ID**
    - **PUT** `http://localhost:8080/transaction/{id}`
    - **Пример**: `http://localhost:8080/transaction/1`
    - **Content-Type**: `application/json`
    - **Тело запроса**:
      ```json
      {
        "amount": 10000,
        "paymentType": "CASH",
        "transactionDate": "2023-02-02T15:30:00"
      }
      ```

6. **Удалить транзакцию**
    - **DELETE** `http://localhost:8080/transaction/{id}`
    - **Пример**: `http://localhost:8080/transaction/1`


## Описание зависимостей в проекте

1. **Spring Boot Starter Data JPA**:  
   `implementation 'org.springframework.boot:spring-boot-starter-data-jpa'`  
   Для работы с базами данных через JPA.


2. **Spring Boot Starter Web**:  
   `implementation 'org.springframework.boot:spring-boot-starter-web'`  
   Для создания веб-приложений и RESTful API.


3. **Liquibase Core**:  
   `implementation 'org.liquibase:liquibase-core'`  
   Для управления миграциями базы данных.


4. **Lombok**:  
   `compileOnly 'org.projectlombok:lombok'`  
   Упрощает написание кода.


5. **PostgreSQL**:  
   `runtimeOnly 'org.postgresql:postgresql'`  
   Драйвер для подключения к базе данных PostgreSQL.


6. **Spring Boot Starter Test**:  
   `testImplementation 'org.springframework.boot:spring-boot-starter-test'`  
   Для тестирования приложений на Spring Boot.


7. **JUnit Platform Launcher**:  
   `testRuntimeOnly 'org.junit.platform:junit-platform-launcher'`  
   Для запуска тестов с использованием JUnit.

   
## TODO в последующих итерациях 
- Добавить индексы в базу данных;
- Добавить интеграционные тесты c использованием @SpringBootTest и TestContainers;
- Добавить Swagger для автоматической генерации документации к контроллерам.