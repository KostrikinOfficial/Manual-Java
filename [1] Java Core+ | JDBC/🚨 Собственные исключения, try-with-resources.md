## 🚨 Собственные исключения, `try-with-resources`
До этого мы использовали готовые исключения: `throw new IllegalArgumentException("Возраст не может быть отрицательным");`

Но в реальном приложении часто появляется специфическая ошибка предметной области.

Например: Недостаточно средств, Пользователь заблокирован, Товар закончился и т.д.

Можно использовать стандартный `IllegalArgumentException`, но иногда гораздо понятнее создать собственный тип.

Например:

    public class InsufficientFundsException extends RuntimeException {

        public InsufficientFundsException(String message) {
            super(message);
        }
    }

Теперь: `throw new InsufficientFundsException("Недостаточно средств");` - мы получили собственный тип исключения.

## ❓ Как создается собственное исключение

### Вариант 1: `extends Exception`

    public class MyException extends Exception {
        public MyException(String message) {
            super(message);
        }
    }

Такое исключение будет checked. Java заставит вызывающий код:
- обработать его через `try/catch`
- или указать `throws`

Использовать когда код реально может и должен разумно обработать ситуацию.

Например: Файл не найден, Ошибка ввода-вывода, Внешний ресурс недоступен.

### Вариант 2: `extends RuntimeException`
    public class MyException extends RuntimeException {
        public MyException(String message) {
            super(message);
        }
    }
Такое исключение будет unchecked. Java не требует обязательно писать: `throws MyException`

Использовать когда проблема чаще говорит о некорректном состоянии или нарушений условий программы.

Например: Недостаточно денег, Недопустимый аргумент, Объект оказался null, Нарушено бизнес-условие.

## 🛑 `try-with-resources`

Представим, что мы открыли ресурс: Файл, Сетевое соединение, Поток, Database Connection.

После работы ресурс нужно закрыть.

### Базовый синтаксис:

    try (FileInputStream input = new FileInputStream("data.txt")) {
    
        // работа с input
    
    } catch (IOException e) {
        System.out.println("Ошибка чтения файла");
    }

Ресурс объявлен внутри скобок `try`. После завершения конструкции Java автоматически закрывает ресурс.

### Можно открыть сразу несколько:

    try (
        FileInputStream input = new FileInputStream("input.txt");
        FileOutputStream output = new FileOutputStream("output.txt")
    ) {
        // работа
    }