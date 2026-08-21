# 🌳 [1.2] Структура Maven-проекта
### Представим, три разработчика создали Java-проект.
### Первый решил: 
    java/
    test/
    resources/
### Второй:
    code/
    tests/
    files/
### Третий:
    src/
    ├── classes/
    ├── tests/
    └── config/
### Технически, можно организовать проект по-разному. Но появится проблема:
### `Как инструмент сборки поймет, где находится основной код, где тесты, а где ресурсы?`
### И здесь Maven предлагает следующее:
### `Если ты следуюешь стандартным соглашениям, тебе не нужно описывать каждую мелочь вручную.`
### Поэтому Maven ожидает стандартную структуру:
    project/
    ├── pom.xml
    └── src/
        ├── main/
        │   ├── java/
        │   └── resources/
        └── test/
            ├── java/
            └── resources/
# 🌲 [1.2.1] Convention over Configuration
### Вместо того, чтобы писать:
### `Maven, основной код находится вот здесь, тесты вот здесь, а ресурсы вот здесь:`
### Мы просто придерживаемся стандартной структуры. Ведь Maven уже знает:
### `src/main/java` - основной Java-код.
### `src/test/java` - тестовый Java-код.
### `src/main/resources` - ресурсы приложения.
### `src/test/resources` - ресурсы, необходимые тестам.
# 👨‍💻 [1.2.2] `src/main/java`
### Это главный каталог с Java-кодом приложения.
### Например:
    src/
        └── main/
            └── java/
                └── com/
                    └── example/
                        └── student/
                            ├── Main.java
                            ├── model/
                            ├── repository/
                            └── service/
### Почему внутри появляются: `com/example/student/`
### Потому что каталог соответствует package
### Например: `package com.example.student;`
### Тогда файл: `Main.java`
### Логично находится: `src/main/java/com/example/student/Main.java`
# 📁 [1.2.3] package и файловая структура
### Здесь важно не смешать две вещи:
### `package com.example.student;` - это часть Java-кода.
### `src/main/java/com/example/student/` - физическое расположение файла.
### Например:
### `src/main/java/com/example/student/model/User.java` может содержать в себе:
    package com.example.student.model;

    public class User {
    }
### Получается:
    путь к файлу
        ↕
    package
# ❓ [1.2.4] Почему `main` называется `main`
### Название: `src/main/` означает основную часть приложения.
### То есть, это всё, что относится к основной программе.
# ⚒️ [1.2.5] `src/main/resources`
### Здесь находятся ресурсы приложения.
### Например:
    src/main/resources/
    ├── application.properties
    ├── config.properties
    └── messages.properties
### Это не Java-код. 
### Например: `app.name=Student Manager`
### Или: `app.language=ru`
### Maven понимает, что это ресурс проекта, и при сборке переносит его в результаты сборки.
# 👨‍💻 [1.2.6] `src/test/java`
### Здесь находятся Java-тесты.
### Например:
    src/test/java/com/example/student/
    └── StudentServiceTest.java
### Это не основной код приложения. Здесь находится код, который проверяет основной код.
## ⚒️ [1.2.7] `src/test/resources`
### Это ресурсы для тестов.
### Например:
    src/test/resources/
    ├── test-data.json
    └── application-test.properties
### Представим, что JUnit нужно прочитать специальный конфигурационный файл.
### Ему необязательно нужен production файл: `src/main/resources/application.properties`
### Можно дать отдельный: `src/test/resources/application-test.properties`
# ☁️ [1.2.8] `target`
### `target` - каталог результатов сборки Maven.
### Например:
    target/
    ├── classes/
    ├── test-classes/
    ├── surefire-reports/
    └── student-manager-1.0-SNAPSHOT.jar
# 🌦️ [1.2.9] `target/classes`
### Здесь находится основной скомпилированный код
### Например: `src/main/java/com/example/Main.java`
### Превращается примерно в: `target/classes/com/example/Main.class`
# 🌨️ [1.2.10] `target/test-classes`
### А тестовый код компилируется отдельно
### Например: `src/test/java/com/example/MainTest.java`
### Получает: `target/test-classes/com/example/MainTest.class`
### Таким образом Maven физически разделяет основной код и тестовый код.
# 📋 [1.2.11] `target/surefire-reports`
### При выполнении тестов Maven обычно использует Maven Surefire Plugin
### Он отвечает за запуск тестов и формирование отчетов.
### После тестирования могут появиться: `target/surefire-reports/`
### С информацией о результатах.
# 🗑️ [1.2.12] Maven Clean Lifecycle
### Ранее мы говорили про default lifecycle с фазами:
### `validate, compile ... , deploy`
### Но у Maven есть несколько lifecycle, один из них: `clean`
### Его задача удалить результаты предыдущей сборки
### Например: `mvn clean` удаляет `target/`