**Task Manager API – Spring Boot**

Prosta aplikacja REST do zarządzania zadaniami.
Projekt zawiera automatyczne testy kontrolera i serwisu (JUnit 5 + MockMvc + Mockito).

**Technologie**

-Java 17
-Spring Boot
-Spring Web
-Spring Data JPA
-H2 Database (in-memory)
-JUnit 5
-MockMvc

🚀 Uruchomienie aplikacji
./mvnw spring-boot:run

Aplikacja będzie dostępna pod adresem:
http://localhost:8080

🔗 Endpointy API
Akcja	Metoda	Endpoint	Body
Pobierz wszystkie zadania	GET	/tasks	–
Dodaj nowe zadanie	POST	/tasks	{ "title": "Zrobić projekt", "completed": false }
🗄️ Konsola bazy H2

Adres: http://localhost:8080/h2-console

JDBC URL: jdbc:h2:mem:testdb

User: sa

Hasło: (puste)

✅ Testy automatyczne

Projekt zawiera dwa główne zestawy testów:

TaskControllerTest – testy kontrolera i endpointów z użyciem MockMvc (bez uruchamiania serwera)

TaskServiceTest – testy logiki biznesowej w serwisie z użyciem mocków repozytorium

🧪 TaskControllerTest

Cel:
Sprawdzenie, czy kontroler poprawnie obsługuje żądania HTTP.

Przykładowe testy:

GET /tasks – zwraca listę zadań i status 200

GET /tasks/{id} – zwraca zadanie po ID lub status 404

POST /tasks – tworzy nowe zadanie, status 201 i zwracany obiekt

PUT /tasks/{id} – aktualizuje zadanie, status 200 i zwracany obiekt

DELETE /tasks/{id} – usuwa zadanie, status 204

Dlaczego ważne:
Testy kontrolera chronią endpointy przed błędami i weryfikują poprawność odpowiedzi HTTP.

🧩 TaskServiceTest

Cel:
Sprawdzenie logiki biznesowej w serwisie TaskService.

Przykładowe testy:

findAllTasks() – zwraca listę wszystkich zadań

findTaskById(id) – zwraca zadanie lub wyrzuca wyjątek, jeśli nie istnieje

createTask(task) – zapisuje nowe zadanie

updateTask(id, task) – aktualizuje istniejące zadanie

deleteTask(id) – usuwa zadanie lub wyrzuca wyjątek, jeśli nie istnieje

Dlaczego ważne:
Zapewniają, że logika biznesowa działa poprawnie niezależnie od kontrolera.

⚡ Uruchamianie testów
W Visual Studio Code

Otwórz projekt w VS Code.

Otwórz Test Explorer (ikona flagi testowej).

VS Code automatycznie wykrywa testy w katalogu:

src/test/java/...


Możesz uruchomić testy:

Klikając Run przy klasie testowej (TaskControllerTest lub TaskServiceTest)

Klikając Run All Tests – uruchomi wszystkie testy w projekcie

Status testów:

Zielony = test przeszedł

Czerwony = test nie przeszedł

Przez Maven (terminal)
./mvnw test


Uruchamia wszystkie testy w katalogu src/test/java

Raporty szczegółowe znajdują się w folderze:

target/surefire-reports

✅ Podsumowanie

TaskControllerTest – testy endpointów i odpowiedzi HTTP

TaskServiceTest – testy logiki biznesowej

Testy można uruchamiać w VS Code lub przez Maven

Chronią projekt przed błędami podczas rozwoju nowych funkcjonalności



**📚 Dokumentacja projektu – Task Manager API**

**1. Opis projektu**

Task Manager API to prosta aplikacja REST do zarządzania zadaniami, napisana w Spring Boot.
Aplikacja umożliwia:

Tworzenie nowych zadań

Pobieranie listy wszystkich zadań

Zarządzanie statusem zadania (completed)

Projekt wykorzystuje wbudowaną bazę H2 (in-memory) i zawiera testy jednostkowe i integracyjne dla wszystkich warstw aplikacji.

**2. Struktura projektu**
src/main/java/com/example/testy/
TestyApplication.java         # Klasa startowa Spring Boot
controller/TaskController.java       # Kontroler REST dla endpointów /tasks
model/Task.java                 # Encja JPA reprezentująca zadanie
repository/TaskRepository.java       # Repozytorium JPA
service/TaskService.java          # Serwis zarządzający logiką biznesową

src/test/java/com/example/testy/
controller/TaskControllerTest.java   # Testy kontrolera z MockMvc
repository/TaskRepositoryTest.java   # Testy repozytorium H2
service/TaskServiceTest.java      # Testy serwisu z mockami
TestyApplicationTests.java    # Test kontekstu Spring Boot

**3. Opis klas i metod**

**3.1 Klasa Task**

Pakiet: com.example.testy.model

Opis: Encja JPA reprezentująca zadanie.

Pola:

Long id – unikalne ID zadania (auto-generowane)

String title – tytuł zadania

boolean completed – status zadania (true = wykonane)

Konstruktor domyślny i parametryczny

Gettery i settery dla wszystkich pól

**3.2 Klasa TaskRepository**

Pakiet: com.example.testy.repository

Opis: Interfejs repozytorium JPA dla encji Task

Metody wbudowane:

findAll() – zwraca wszystkie zadania

save(Task task) – zapisuje nowe zadanie

deleteById(Long id) – usuwa zadanie po ID

**3.3 Klasa TaskService**

Pakiet: com.example.testy.service

Opis: Warstwa serwisu zarządzająca logiką biznesową.

Metody:

List<Task> getAllTasks() – pobiera wszystkie zadania

Task addTask(Task task) – dodaje nowe zadanie do repozytorium

**3.4 Klasa TaskController**

Pakiet: com.example.testy.controller

Opis: REST controller obsługujący endpointy /tasks.

Endpointy:

GET /tasks – zwraca listę wszystkich zadań

POST /tasks – dodaje nowe zadanie, przyjmuje JSON { "title": "...", "completed": false }

**3.5 Klasa TestyApplication**

Pakiet: com.example.testy

Opis: Klasa startowa Spring Boot

**4. Endpointy API**
Metoda	Endpoint	Opis	Body
GET	/tasks	Pobierz wszystkie zadania	–
POST	/tasks	Dodaj nowe zadanie	{ "title": "Zrobić projekt", "completed": false }

**5. Konfiguracja bazy danych**

Typ: H2 (in-memory)

Konsola H2: http://localhost:8080/h2-console

JDBC URL: jdbc:h2:mem:testdb

User: sa

Hasło: (puste)

Dodatkowo w application.properties:

spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.hibernate.ddl-auto=create-drop
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
server.port=8080

**6. Testy**

Projekt zawiera testy dla wszystkich warstw: kontroler, serwis, repozytorium.

**6.1 TaskControllerTest**

Cel: testowanie endpointów REST z MockMvc

Przykłady testów:

Pobranie listy zadań (GET /tasks)

Dodanie nowego zadania (POST /tasks)

Mockowanie: TaskService jest mockowane (@MockBean)

Framework: JUnit 5 + MockMvc

**6.2 TaskServiceTest**

Cel: testowanie logiki biznesowej

Metody testowane:

getAllTasks()

addTask(Task task)

Mockowanie: TaskRepository jest mockowane (@Mock)

Framework: JUnit 5 + Mockito

**6.3 TaskRepositoryTest**

Cel: testowanie operacji na bazie H2

Przykład testu: zapis i odczyt zadania (save() i findAll())

Framework: JUnit 5 + Spring Data JPA (@DataJpaTest)

**6.4 Testy kontekstu Spring Boot**

Klasa: TestyApplicationTests

Cel: sprawdzenie, czy kontekst Spring Boot w ogóle się uruchamia

7. Uruchamianie testów

**7.1 W Visual Studio Code**

Otwórz projekt w VS Code

Panel Test Explorer automatycznie wykrywa testy w src/test/java

Kliknij Run przy klasie testowej lub Run All Tests

**7.2 Przez Maven**
./mvnw test


Raporty szczegółowe w target/surefire-reports

**8. Podsumowanie**

Warstwa modelu: Task – encja JPA

Warstwa repozytorium: TaskRepository – dostęp do bazy danych

Warstwa serwisu: TaskService – logika biznesowa

Warstwa kontrolera: TaskController – endpointy REST

Testy: kontroler, serwis, repozytorium, kontekst Spring Boot

Baza danych: H2 (in-memory) z konsolą webową
