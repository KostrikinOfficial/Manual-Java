## ☄️ `throw`
### `throw` выбрасывает конкретное исключение прямо сейчас.
До этого мы в основном ловили исключения через `try`, `catch`

Но Java позволяет нам самим сообщить: Возникла ситуация, которую я считаю ошибкой.

Для используется: `throw`, например:

    if (age < 0) {
        throw new IllegalArgumentException("Возраст не может быть отрицательным");
    }

Здесь мы сами создаем объект исключения: `IllegalArgumentException(...)`

И выбрасываем его: `throw ...`

## 🛡️ `throws`
### `throws` указывает в сигнатуре метода, что метод может выбросить исключение.
Например:

    public void readFile() throws IOException {
        ...
    }

Метод сообщает вызывающему коду: При вызове этого метода может возникнуть `IOException`, поэтому тебе нужно учитывать это.

Например:

    public void methodA() throws IOException {
        readData();
    }

Если `readData()` может выбросить checked exception, то `methodA()` должен либо:

- обработать исключение через `try/catch`
- либо тоже объявить `throws`

## 📁 Checked Exceptions
### Checked Exceptions - это...
Исключения, которые Java требует учитывать на этапе компиляции.

Они часто используются там, где проблема является является внешней и потенциально ожидаемой.

Например: 
- Файл отсутствует, 
- Сетевое соединение недоступно, 
- Ошибка ввода-вывода.

Типичный пример: `IOException`

Например:

    public void readFile() throws IOException {
        ...
    }

Компилятор следит, чтобы вызывающий код не проигнорировал это исключение.

## ⚡ Unchecked Exceptions
### Unckecked Exceptions - это...
Исключения, которые Java не заставляет объявлять через `throws` или обязательно ловить. 

Они находятся в ветке: `RuntimeException`

Например:

    ArithmeticException
    NullPointerException
    IllegalArgumentException
    NumberFormatException

Можно написать:

    public void divide(int a, int b) {
        if (b == 0) {
            throw new ArithmeticException();
        }
    }

Не нужно: `public void divide(int a, int b) throws ArithmeticException`

Это допустимо, но бессмысленно, потому что `ArithmeticException` - unchecked.

## 🌳 Общая иерархия
### Упрощённо:
    Throwable
    ├── Error
    └── Exception
    ├── RuntimeException
    │   ├── NullPointerException
    │   ├── ArithmeticException
    │   └── IllegalArgumentException
    │
    └── IOException
        SQLException
        ...

Если исключение относится к `RuntimeException` - unchecked.

Если это `Exception`, но не `RuntimeException` - обычно checked.

