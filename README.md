# Calculator

Простий калькулятор на основі Rust, який підтримує базові арифметичні операції, дужки та унарний мінус. Для парсингу використовується бібліотека `pest`, а для обробки пріоритету операторів — Pratt-парсер.

## Особливості
- **Арифметичні операції:** Додавання, віднімання, множення, ділення.
- **Пріоритет операторів:** Обробляє пріоритет для `*`, `/` (вищий) над `+`, `-` (нижчий).
- **Унарний мінус:** Підтримує вирази типу `-(2 + 5)`.
- **Дужки:** Дозволяє групувати вирази за допомогою `()`.

## Приклад використання
### Вхідні дані
```text
1 + 2 * 3
-(4 + 5) * 2
```

### Результат
```text
Result: 7
Result: -18
```

## Встановлення
1. Клонуйте репозиторій:
   ```bash
   git clone https://github.com/yourusername/calculator.git
   cd calculator
   ```
2. Зберіть проект:
   ```bash
   cargo build
   ```

## Запуск калькулятора
Запустіть програму за допомогою:
```bash
cargo run
```

Після цього введіть математичні вирази в терміналі рядок за рядком.

## Граматика
Правила для парсингу калькулятора визначені у файлі `calculator.pest`:
```pest
WHITESPACE = _{ " " }

integer = @{ ASCII_DIGIT+ }

add = { "+" }
subtract = { "-" }
multiply = { "*" }
divide = { "/" }

bin_op = _{ add | subtract | multiply | divide }
unary_minus = { "-" }
primary = _{ integer | "(" ~ expr ~ ")" }
atom = _{ unary_minus? ~ primary }
expr = _{ atom ~ (bin_op ~ atom)* }
equation = _{ SOI ~ expr ~ EOI }
```
