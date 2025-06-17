# ✅ Урок 45: Налагодження та тестування коду

---
<img src="main_image.png" alt="pygame" width="1500">

## Зміст уроку:

1. [Сьогодні на уроці](#1-сьогодні-на-уроці)
2. [Налагодження (`Debugging`)](#2-налагодження-debugging)
3. [Тестування (`Testing`)](#3-тестування-testing)
4. [Декоратор (`Decorator`)](#4-декоратор-decorator)
5. [Реалізація](#5-реалізація-implementation)
6. [Підведення підсумків 🚀](#6-підведення-підсумків-)

> 🔗 Useful Links:

- [Logging facility for Python](https://docs.python.org/uk/3.12/library/logging.html)
- [Decorator in Python](https://acode.com.ua/decorators-python/)
- [Decorator](https://refactoring.guru/uk/design-patterns/decorator/python/example)

---

## 1. Сьогодні на уроці

> 💡 На цьому уроці ми розглянемо важливі навички для будь-якого програміста: **налагодження** та **тестування** коду,
> які допомагають зробити код стабільним, зручним для підтримки та легким у використанні.

Помилки можуть траплятися в будь-якому проекті, тому вміння швидко їх знайти та виправити значно економить час і
підвищує якість програми.

Налагодження і логування допомогає контролювати процес виконання коду, виявляти слабкі місця та зробити програму більш
зрозумілою для інших розробників.

Тестування дозволяє впевнитися, що програма працює як очікувалося, і що зміни в коді не призведуть до нових помилок.

> 💡 На цьому уроці ми розглянемо наступні теми:

- Що таке налагодження (`debugging`) і чому це важливо.
- Огляд інструментів для налагодження: `print`, `pdb`, `logging`.
- Приклади використання `pdb` для встановлення точок зупинки у коді.
- Налаштування базового логування (`logging`) для **TelegramBot**.

[Повернутися до змісту](#зміст-уроку)

---

## 2. Налагодження (`Debugging`)

> 💡 Налагодження (`debugging`) - це процес **виявлення** та **виправлення помилок** в коді (програмі).

### Популярні інструменти для `debugging`:

- `print()`
- `pdb`
- `logging`

### Вбудована функція `print()`:

Вбудована функція `print()` - це один з найпоширеніших способів налагодження коду Python, який може виводити в консоль
значення **змінних**, **функцій** та **інших блоків** коду у різних точках програми, що може допомогти визначити, в
якому рядку коду виникає **помилка**.

Однак цей метод може стати **нудним** і **трудомістким** для великих і складних програм.

### 🧩 For Example:

```python
def add(a, b):
    print(f"a: {a}, b: {b}")  # Виведення значень змінних
    return a + b


result = add(3, 5)
print(f"Result: {result}")
```

### Вбудована бібліотека `pdb`:

Вбудована бібліотека `pdb` - це інструмент налагодження, який надає набір команд для перевірки **змінних**, **функцій**
та **інших блоків** коду, а також **відстеження** та **керування** процесом виконання програми.

Функція `set_trace()` використовується для встановлення **точки зупинки** в коді, що зупиняє виконання програми та
дозволяє перевірити стан програми в цей момент.

### 🧩 For Example:

Після запуску, програма зупиняється на рядку `pdb.set_trace()`, а у терміналі з'явиться командний рядок `Pdb`.

```python
import pdb


def my_function():
    a = 1
    b = 2
    c = a + b
    pdb.set_trace()  # Встановлення точки зупинки
    print(c)


my_function()
```

В момент зупинки програми, ви можете вводити різні команди для перевірки стану програми і контролю за її виконання.

Найпоширеніші команди `pdb`:

- `n` або `next`: Виконати наступний рядок коду і перейти на наступний рядок.
- `s` або `step`: Перехід до виклику функції.
- `c` або `continue`: Продовжити виконання, доки не буде досягнуто точки зупинки або не відбудеться вихід з програми.
- `l` або `list`: Вивести вихідний код поточного файлу.
- `w` або `where`: Вивести трасування стеку і номер поточного рядка.
- `p` або `print`: Вивести значення виразу.
- `h` або `help`: Показати список доступних команд.

### Логування (`logging`):

Вбудована бібліотека `logging` - це інструмент, який дозволяє **реєструвати** (зберігати в журнал) інформацію про події,
що відбуваються під час виконання програми.

### 🧩 For Example:

```python
# Імпортуємо модуль logging для роботи з логуванням
import logging

"""
Налаштування базової конфігурації логування
- filename: ім'я файлу, куди будуть записуватися логи
- level: рівень важливості повідомлень, які будуть логуватися
- format: формат кожного лог-запису, включаючи час, ім'я логера, рівень важливості та повідомлення
"""

logging.basicConfig(
    filename="my_logging.log",
    level=logging.INFO,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'
)

# Створюємо об'єкт logger з ім'ям поточного модуля
logger = logging.getLogger(__name__)


def main():
    # Логуємо повідомлення про початок роботи
    logger.info("Started")

    # Логуємо повідомлення про виконання якоїсь дії
    logger.info(f"Add some numbers {7 + 3}")

    # Логуємо повідомлення про завершення роботи
    logger.info("Finished")


if __name__ == "__main__":
    main()
```

[Повернутися до змісту](#зміст-уроку)

---

## 3. Тестування (`Testing`)

> 💡 Тестування (`Testing`) - це процес оцінки системи або її окремого компонента з метою з'ясування, чи задовольняють
> вони очікуваним вимогам або ні.

Python пропонує декілька популярних бібліотек для автоматизації тестування: `unittest` та `pytest`.

**Мануальне** тестування виконується **вручну**, власними очима крок за кроком перевіряються очікувані результати роботи
**функцій**, значень **змінних**, інших блоків та модулів програми.

**Автоматизоване** тестування надає можливість заощадити час на перевірці **очікуваних** результатів всіх **елементів**
програми та унеможливлює ймовірність помилок з боку **людського** фактору.

### 💡 Бібліотека `Unittest`:

Бібліотека `Unittest` входить до складу стандартної бібліотеки Python та надає різноманітний набір інструментів для
написання та запуску автоматизованих тестів.

Бібліотека `Unittest` основана на **class-base** підході, тому щоб використовувати `unittest` необхідно **створити**
**клас**, який має успадковуватися від `unittest.TestCase` та визначити **тестові методи** в цьому класі.

- Назва **методів-тестів** повинна починатися з префіксу `test_`.
- `Unittest` надає можливість використовувати різні **методи ствердження**, надані класом `TestCase`, для перевірки
  результатів роботи коду.

### 🧩 For Example:

Необхідно створити тестовий приклад для функції `add`, яка отримує `2` числа і повертає їх **суму**.

- Створити тестовий клас `TestAdd`.
- Успадкувати `TestAdd` від `unittest.TestCase`.
- Визначити **тестові методи** в цьому класі: `test_add_integers`,`test_add_floats`, `test_add_strings`.
- Кожен **метод** має викликати функцію `add` з різними вхідними даними.
- Кожен **метод** має використовувати один з **методів ствердження** `assert`, які надає клас `unittest.TestCase`, для
  порівняння **актуального** та **очікуваного** результату.

Запустити тестовий приклад можна викликавши `unittest.main()` в середині скрипта, або викликати в консолі наступну
команду `python -m unittest module_name.py`.

```python
import unittest


def add(a, b):
    return a + b


class TestAdd(unittest.TestCase):
    def test_add_integers(self):
        result = add(1, 2)
        self.assertEqual(result, 3)

    def test_add_floats(self):
        result = add(0.1, 0.2)
        self.assertAlmostEqual(result, 0.3)

    def test_add_strings(self):
        result = add("hello", "world")
        self.assertEqual(result, "helloworld")


if __name__ == '__main__':
    unittest.main()
```

Бібліотека `Unittest` надає ряд **методів ствердження**, які використовуються для **порівняння актуального та
очікуваного** результату роботи тестового методу.

### 💡 Найпоширеніші методи ствердження:

- `assertEqual(a, b)`: перевіряє, що `a == b`
- `assertTrue(x)`: перевіряє, що `bool(x)` має значення `True`
- `assertFalse(x)`: перевіряє, що `bool(x)` має значення `False`
- `assertIs(a, b)`: перевіряє, що `a` є `b` (чи є два об'єкти одним і тим же об'єктом в пам'яті)
- `assertIsNone(x)`: перевіряє, що `x` є `None`
- `assertIn(a, b)`: перевіряє, що `a` знаходиться в `b`
- `assertIsInstance(a, b)`: перевіряє, що `isinstance(a, b)` рівне `True`

Бібліотека `Unittest` надає можливість використовувати методи `setUp()` і `tearDown()` для виконання будь-яких завдань з
**налаштування** або **очищення**, які необхідно виконати **до** або **після** запуску кожного тестового методу.

### 💡 Бібліотека `Pytest`:

Бібліотека `Pytest` - це багатофункціональний інструмент (фреймворк) для автоматичного тестування, який має простий та
зручний синтаксис, який полегшує написання та розуміння тестів.

Бібліотеку `Pytest` необхідно **інсталювати** (наприклад, за допомогою менеджера пакетів `pip`)

```text
pip install pytest
```

За замовчуванням, `pytest` здійснює пошук тестових файлів у проекті, які відповідають певному шаблону, та запускає
тестові функції, визначені у цих тестових файлах.

- Наприклад, проєкт містить **файл** з кодом, який має **назву** `my_module.py`.
- В цьому випадку, `pytest` буде здійснювати пошук файлу з назвою `test_my_module.py` та запускатиме функції тестування,
  визначені у цьому файлі.

> 💡 Функції тестування мають бути визначені з префіксом `test_`

Наприклад, якщо у вас є функція з назвою `add` у файлі `my_module.py`, вам слід створити тестову функцію з назвою
`test_add` у файлі `test_my_module.py`

### 🧩 For Example:

```python
def add(a, b):
    return a + b


def test_add():
    assert add(1, 2) == 3
```

Запустити тести можна в терміналі, за допомогою наступних команд:

```text
pytest
pytest module_name.py
```

`Pytest` автоматично запустить всі функції тестування у вашому проекті, надасть детальну інформацію про будь-які
збої або помилки, що виникають під час тестування, що полегшить виявлення та виправлення будь-яких проблем.


> 💡 **Фікстури** `pytest` - це невеликі фрагменти коду, які застосовуються для **налаштування** та **очищення**
> ресурсів, які використовуються тестами.

Наприклад, якщо тести покладаються на з'єднання з базою даних, ви можете використати фікстури для налаштування з'єднання
перед запуском тесту, а потім закрити з'єднання після завершення тесту.

Загалом, `pytest` надає ряд вбудованих функцій, наприклад **параметризацію** тестів та велику кількість **плагінів**,
які можна використовувати для розширення функціональності даної бібліотеки.

[Повернутися до змісту](#зміст-уроку)

---

## 4. Декоратор (`Decorator`)

Для додаткової інформативності нашого **TelegramBot**, додамо **логування** назв функцій, які відповідають за обробку
подій в нашому застосунку.

Для реалізації цього завдання, скористаємось можливостями **декораторів**.

> 💡 **Декоратор** (`Decorator`) - це функція, яка приймає та динамічно додає нову функціональність до іншої функції.

- Декоратор також називають **патерном** (**шаблоном**) проектування.
- Декоратор не змінює оригінальну функцію, а лише модифікує (розширює) її новою функціональністю, використовуючи
  функції-обгортки.
- Декоратори можна вкладати один в один, створюючи ланцюжок декораторів, що послідовно застосовуються до функції.
- Декоратори можна використовувати повторно для різних функцій, економлячи час та код.
- Декоратори роблять код більш читабельним, чітко відокремлюючи базову функціональність від додаткової поведінки, що
  додається декораторами.

### Приклади використання декораторів:

- **Авторизація**: Декоратор може перевіряти, чи має користувач доступ до виконання функції, перш ніж дозволити їй
  запуститися.
- **Кешування**: Декоратор може кешувати результати функції, щоб уникнути повторних обчислень.
- **Ведення журналу**: Декоратор може записувати інформацію про виклики функції, наприклад, час виклику, аргументи та
  результати.
- **Оброблення помилок**: Декоратор може обробляти винятки, що виникають у функції, та вживати відповідних заходів.

[Повернутися до змісту](#зміст-уроку)

---

## 5. Реалізація (`Implementation`)

> 💡 Після того як ми обрали інструменти для **налагодження** та **тестування**, необхідно виконати їх реалізацію в
> проєкті.

Зверніть увагу, що бібліотека `aiogram` за замовчуванням виконала інтеграцію модуля `logging`, у головний файл нашого
застосунку `bot.py`, а в середині конструкції `if __name__ == "__main__"` відбувається налаштування рівня логування та
потоку виводу логів.

```python
import logging

...

if __name__ == "__main__":
    logging.basicConfig(level=logging.INFO, stream=sys.stdout)
    asyncio.run(main())
```

При кожному виклику **функцій-обробників** модуля `bot.py`, спрацьовують методи `log`, `info`, `debug`, `error`,
`exception` - саме цю інформацію ми і бачимо в терміналі, під час роботи **TelegramBot**.

В конструкції `if __name__ == "__main__"` присутні інформативні (`INFO`) логи, які обробляє `aiogram.dispatcher`,
поведінку якого важливо фіксувати і аналізувати кожного разу коли було внесено зміни в застосунок.

### Основний синтаксис логів:

```text
<level>:<object>:<message>
```

- `level`: рівень логування (`INFO` -> `DEBUG` -> `WARN/WARNING` -> `ERROR` -> `EXCEPTION` -> `CRITICAL`)
- `object`: екземпляр класу, функція, метод або модуль.
- `message`: повідомлення яке містить `logger`.

Необхідно створити файл `logger.py`, в якому потрібно реалізувати власний декоратор `async_log_function()`, для
**журналювання** функцій (обробників подій) нашого проєкту:

```python
# logger.py
import logging
from functools import wraps
from typing import Callable, Any

# Налаштування логування
logger = logging.getLogger(__name__)
logger.setLevel(logging.INFO)

# Форматування повідомлень логування
formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')

# Обробник для запису логів у файл
file_handler = logging.FileHandler('logger_journal.log', mode='a')
file_handler.setFormatter(formatter)

# Обробник для виведення логів у консоль
console_handler = logging.StreamHandler()
console_handler.setFormatter(formatter)

# Додавання обробників до логера
logger.addHandler(file_handler)
logger.addHandler(console_handler)


def async_log_function(func: Callable) -> Callable:
    """Декоратор для логування викликів асинхронних функцій."""

    @wraps(func)
    async def wrapper(*args, **kwargs) -> Any:
        logger.info(f"Виклик функції '{func.__name__}' з аргументами: {args}, {kwargs}")
        try:
            result = await func(*args, **kwargs)
            logger.info(f"Функція '{func.__name__}' успішно завершила роботу")
            return result
        except Exception as e:
            logger.error(f"Помилка у функції '{func.__name__}': {e}", exc_info=True)
            raise

    return wrapper
```

- Імпортуємо модуль `logging` для налаштування логування.
- Імпортуємо `wraps` з модуля `functools`, щоб зберегти метадані оригінальної функції при використанні декоратора.
- Імпортуємо типи `Callable` та `Any` з модуля `typing` для анотації типів.
- Створюємо логер з ім'ям поточного модуля за допомогою `logging.getLogger(__name__)`.
- Встановлюємо рівень логування на `INFO`, щоб логер записував повідомлення з рівнем `INFO` і вище.
- Визначаємо формат повідомлень логування, який включає час, ім'я логера, рівень логування та повідомлення.
- Створюємо обробник `FileHandler`, який записує логи у файл `logger_journal.log` в режимі додавання (`mode='a'`).
- Встановлюємо формат повідомлень для обробника файлу.
- Створюємо обробник `StreamHandler`, який виводить логи в консоль.
- Встановлюємо формат повідомлень для консольного обробника.
- Додаємо обробники файлу та консолі до логера, щоб логи записувалися і в файл, і виводилися на консоль.
- Визначаємо декоратор `async_log_function`, який логує виклики асинхронних функцій.
- Функція `wrapper` є обгорткою, яка логує виклик функції з її аргументами.
- Всередині блоку `try`, викликається оригінальна функція func з аргументами, і логується успішне завершення.
- Якщо виникає помилка, вона логується з інформацією про виняток, і виняток знову піднімається.

Необхідно імпортувати декоратор `async_log_function()` в модуль `bot.py`:

```python
from logger import async_log_function
```

Необхідно додати декоратор `@async_log_function` до всіх функцій-обробників подій, які знаходяться в модулі `bot.py`.

> ⚠️ Зверніть увагу, що декоратор `@async_log_function` необхідно розмістити між декоратором `aiogram` та оголошенням
> функції, для того щоб не порушити порядок виклику, який відбувається **зверху донизу**, так само як і всі інструкції у
> Python.

Якщо поміняти декоратори місцями, то `@async_log_function` буде обертати функцію-обробник, а
`@dp.message(START_COMMAND)` буде намагатися обробити результат обгортки, а не саму функцію.

В такому випадку `@dp.message(START_COMMAND)` не зможе правильно декорувати функцію як обробник повідомлень, оскільки
він отримає на вході **вже обгорнуту** функцію, а не **оригінальну**.

### 🧩 For Example:

- Декоратор `@dp.message(START_COMMAND)` повинен обертати функцію-декоратор `@async_log_function`.
- Декоратор `@async_log_function` повинен обертати функцію `async def start`.
- Якщо порушити порядок декорування, то команда `/start` буде оброблена **не коректно**.

```python
@dp.message(START_COMMAND)
@async_log_function
async def start(message: Message) -> None:
    pass
```

✅ Оновлений код модуля `bot.py`:

```python
# Імпортуємо необхідні модулі
import asyncio  # Для асинхронного програмування
import logging  # Для логування подій
import sys  # Для доступу до деяких змінних та функцій, пов'язаних з інтерпретатором Python

# Імпортуємо токен бота з конфігураційного файлу
from config import BOT_TOKEN as TOKEN

# Імпортуємо необхідні класи та функції з бібліотеки aiogram
from aiogram import Bot, Dispatcher, html
from aiogram.client.default import DefaultBotProperties
from aiogram.enums import ParseMode
from aiogram.filters import Command
from aiogram.types import Message, CallbackQuery, URLInputFile, ReplyKeyboardRemove
from aiogram.fsm.context import FSMContext
from aiogram.fsm.state import State, StatesGroup
from commands import FILMS_COMMAND, START_COMMAND, FILM_CREATE_COMMAND, BOT_COMMANDS
from data import get_films, add_film, save_films
from keyboards import films_keyboard_markup, FilmCallback
from models import Film
from logger import async_log_function

# Ініціалізуємо диспетчер для обробки оновлень
dp = Dispatcher()


# Форма для отримання інформації про фільми від користувача
class FilmForm(StatesGroup):
    name = State()
    description = State()
    rating = State()
    genre = State()
    actors = State()
    poster = State()


class FilmStates(StatesGroup):
    search_query = State()
    filter_criteria = State()
    delete_query = State()
    edit_query = State()
    edit_description = State()
    rate_query = State()
    set_rating = State()


# Обробник для команди /start
@dp.message(Command("start"))
@async_log_function
async def start(message: Message) -> None:
    await message.answer(
        f"Hello🖐, {html.bold(message.from_user.full_name)}!\n"
        "I'm your first Telegram Bot 🥳"
    )


# Обробник для команди /films
@dp.message(FILMS_COMMAND)
@async_log_function
async def films(message: Message) -> None:
    data = get_films()
    markup = films_keyboard_markup(films_list=data)
    await message.answer(
        f"<b>Список фільмів: 🎬</b>\nОберіть фільм, щоб отримати інформацію про нього.",
        reply_markup=markup
    )


# Обробник зворотного виклику для фільмів
@dp.callback_query(FilmCallback.filter())
@async_log_function
async def callback_film(callback: CallbackQuery, callback_data: FilmCallback) -> None:
    # Отримуємо ID фільму з даних зворотного виклику
    film_id = callback_data.id
    # Отримуємо дані про конкретний фільм за його ID
    film_data = get_films(film_id=film_id)
    # Створюємо об'єкт фільму
    film = Film(**film_data)

    # Формуємо текст повідомлення з деталями про фільм
    text = (
        f"<b>Фільм:</b> {film.name}\n"
        f"<b>Опис:</b> {film.description}\n"
        f"<b>Рейтинг:</b> {film.rating}\n"
        f"<b>Жанр:</b> {film.genre}\n"
        f"<b>Актори:</b> {', '.join(film.actors)}\n"
    )

    # Відправляємо фото з постером фільму та текстом з деталями
    await callback.message.answer_photo(
        caption=text,
        photo=URLInputFile(
            film.poster,
            filename=f"{film.name}_poster.{film.poster.split('.')[-1]}"
        )
    )


# Функції-обробники для кожного поля форми отримання інформації від користувача
@dp.message(FILM_CREATE_COMMAND)
@async_log_function
async def film_create(message: Message, state: FSMContext) -> None:
    await state.set_state(FilmForm.name)
    await message.answer(
        f"<b>Введіть назву фільму ...</b>",
        reply_markup=ReplyKeyboardRemove(),
    )


@dp.message(FilmForm.name)
@async_log_function
async def film_name(message: Message, state: FSMContext) -> None:
    await state.update_data(name=message.text)
    await state.set_state(FilmForm.description)
    await message.answer(
        f"<b>Введіть опис фільму ...</b>",
        reply_markup=ReplyKeyboardRemove(),
    )


@dp.message(FilmForm.description)
@async_log_function
async def film_description(message: Message, state: FSMContext) -> None:
    await state.update_data(description=message.text)
    await state.set_state(FilmForm.rating)
    await message.answer(
        f"<b>Вкажіть рейтинг фільму (від 0 до 10) ...</b>",
        reply_markup=ReplyKeyboardRemove(),
    )


@dp.message(FilmForm.rating)
@async_log_function
async def film_rating(message: Message, state: FSMContext) -> None:
    await state.update_data(rating=float(message.text))
    await state.set_state(FilmForm.genre)
    await message.answer(
        f"<b>Введіть жанр фільму ...</b>",
        reply_markup=ReplyKeyboardRemove(),
    )


@dp.message(FilmForm.genre)
@async_log_function
async def film_genre(message: Message, state: FSMContext) -> None:
    await state.update_data(genre=message.text)
    await state.set_state(FilmForm.actors)
    await message.answer(
        text=f"<b>Введіть акторів фільму через `, ` \n⚠️ (Обов'язкова кома та відступ після неї)</b>",
        reply_markup=ReplyKeyboardRemove(),
    )


@dp.message(FilmForm.actors)
@async_log_function
async def film_actors(message: Message, state: FSMContext) -> None:
    await state.update_data(actors=[x for x in message.text.split(", ")])
    await state.set_state(FilmForm.poster)
    await message.answer(
        f"<b>Введіть посилання на постер фільму ...</b>",
        reply_markup=ReplyKeyboardRemove(),
    )


@dp.message(FilmForm.poster)
@async_log_function
async def film_poster(message: Message, state: FSMContext) -> None:
    data = await state.update_data(poster=message.text)
    film = Film(**data)
    add_film(film.model_dump())
    await state.clear()
    await message.answer(
        f"<b>Фільм {film.name} успішно додано ✅</b>",
        reply_markup=ReplyKeyboardRemove(),
    )


# Пошук фільму за назвою
@dp.message(Command("search_film"))
async def search_film(message: Message, state: FSMContext):
    await state.set_state(FilmStates.search_query)
    await message.reply("<b>Введіть назву фільму для пошуку:</b>")


@dp.message(FilmStates.search_query)
@async_log_function
async def get_search_query(message: Message, state: FSMContext):
    query = message.text.lower()
    films_data = get_films()
    results = [film for film in films_data if query in film['name'].lower()]

    if results:
        for film_data in results:
            # Створюємо об'єкт Film з даних
            film = Film(**film_data)
            # Формуємо текст повідомлення з деталями про фільм
            text = (f"<b>Фільм:</b> {film.name}\n"
                    f"<b>Опис:</b> {film.description}\n"
                    f"<b>Рейтинг:</b> {film.rating}\n"
                    f"<b>Жанр:</b> {film.genre}\n"
                    f"<b>Актори:</b> {', '.join(film.actors)}\n")

            # Відправляємо повідомлення з фото та інформацією
            await message.answer_photo(
                caption=text,
                photo=URLInputFile(
                    film.poster,
                    filename=f"{film.name}_poster.{film.poster.split('.')[-1]}"
                )
            )
    else:
        await message.reply("<b>Фільм не знайдено!</b>")

    await state.clear()


# Фільтрація фільмів за жанром
@dp.message(Command("filter_films"))
@async_log_function
async def filter_film(message: Message, state: FSMContext):
    await state.set_state(FilmStates.filter_criteria)
    await message.reply("<b>Введіть жанр фільму для фільтрації:</b>")


@dp.message(FilmStates.filter_criteria)
@async_log_function
async def get_filter_criteria(message: Message, state: FSMContext):
    criteria = message.text.lower()
    films_data = get_films()

    # Фільтруємо фільми за жанром
    filtered = list(filter(
        lambda film: criteria in film['genre'].lower(),
        films_data
    ))

    if filtered:
        for film_data in filtered:
            # Створюємо об'єкт Film з даних
            film = Film(**film_data)
            # Формуємо текст повідомлення з деталями про фільм
            text = (f"<b>Фільм:</b> {film.name}\n"
                    f"<b>Опис:</b> {film.description}\n"
                    f"<b>Рейтинг:</b> {film.rating}\n"
                    f"<b>Жанр:</b> {film.genre}\n"
                    f"<b>Актори:</b> {', '.join(film.actors)}\n")

            # Відправляємо повідомлення з фото та інформацією
            await message.answer_photo(
                caption=text,
                photo=URLInputFile(
                    film.poster,
                    filename=f"{film.name}_poster.{film.poster.split('.')[-1]}"
                )
            )
    else:
        await message.reply("<b>Фільмів за вказаним жанром не знайдено.</b>")

    await state.clear()


# Видалення фільму за назвою
@dp.message(Command("delete_film"))
@async_log_function
async def delete_film(message: Message, state: FSMContext):
    await message.reply("<b>Введіть назву фільму, який бажаєте видалити:</b>")
    await state.set_state(FilmStates.delete_query)


@dp.message(FilmStates.delete_query)
@async_log_function
async def get_delete_query(message: Message, state: FSMContext):
    film_to_delete = message.text.lower()
    films_data = get_films()

    # Шукаємо фільм за назвою
    for film in films_data:
        if film_to_delete == film['name'].lower():
            films_data.remove(film)
            save_films(films_data)  # Зберігаємо оновлений список фільмів
            await message.reply(f"<b>Фільм '{film['name']}' видалено ✅</b>")
            await state.clear()
            return

    await message.reply("<b>Фільм не знайдено!</b>")
    await state.clear()


# Редагування інформації про фільм
@dp.message(Command("edit_film"))
@async_log_function
async def edit_film(message: Message, state: FSMContext):
    films_data = get_films()
    if not films_data:
        await message.reply("<b>Список фільмів порожній. Немає що редагувати.</b>")
        return

    film_names = "\n".join([f"- {film['name']}" for film in films_data])
    await message.reply(
        "<b>Введіть назву фільму, який бажаєте редагувати:</b>\n"
        f"Доступні фільми:\n{film_names}"
    )
    await state.set_state(FilmStates.edit_query)


@dp.message(FilmStates.edit_query)
@async_log_function
async def get_edit_query(message: Message, state: FSMContext):
    film_name = message.text.strip()
    films_data = get_films()

    film_found = None
    for film in films_data:
        if film_name.lower() == film['name'].lower():
            film_found = film
            break

    if not film_found:
        await message.reply("<b>Фільм не знайдено!</b>")
        await state.clear()
        return

    await state.update_data(film=film_found, films_data=films_data)
    await message.reply(
        "<b>Введіть поле для редагування та нове значення у форматі:</b>\n"
        "<code>поле|нове значення</code>\n\n"
        "<b>Доступні поля:</b> name, description, rating, genre, actors, poster\n"
        "<b>Приклад:</b> <code>rating|9.5</code>"
    )
    await state.set_state(FilmStates.edit_description)


@dp.message(FilmStates.edit_description)
@async_log_function
async def process_edit(message: Message, state: FSMContext):
    try:
        data = await state.get_data()
        film = data['film']
        films_data = data['films_data']

        if '|' not in message.text:
            raise ValueError("Невірний формат. Використовуйте '|' для розділення поля та значення")

        field, new_value = message.text.split('|', 1)
        field = field.strip().lower()
        new_value = new_value.strip()

        valid_fields = ['name', 'description', 'rating', 'genre', 'actors', 'poster']
        if field not in valid_fields:
            raise ValueError(f"Невірне поле. Доступні: {', '.join(valid_fields)}")

        # Обробка спеціальних типів даних
        if field == 'rating':
            try:
                new_value = float(new_value)
                if not 0 <= new_value <= 10:
                    raise ValueError("Рейтинг повинен бути від 0 до 10")
            except ValueError:
                raise ValueError("Рейтинг повинен бути числом (наприклад, 8.5)")
        elif field == 'actors':
            new_value = [actor.strip() for actor in new_value.split(',')]

        # Оновлення поля
        for f in films_data:
            if f['name'] == film['name']:
                f[field] = new_value
                break

        save_films(films_data)
        await message.reply(f"<b>Фільм '{film['name']}' успішно оновлено!</b>\n"
                            f"<b>{field}:</b> {new_value}")
        await state.clear()

    except Exception as e:
        await message.reply(f"<b>Помилка:</b> {str(e)}\n"
                            "<b>Використовуйте формат:</b>\n"
                            "<code>поле|нове значення</code>\n"
                            "<b>Приклад:</b> <code>rating|9.5</code>")
        await state.clear()


# Функція для рекомендацій
@dp.message(Command("recommend_film"))
@async_log_function
async def recommend_film(message: Message) -> None:
    films_data = get_films()

    # Фільтруємо фільми з рейтингом та сортуємо за спаданням рейтингу
    rated_films = [film for film in films_data if film.get('rating') is not None]
    if not rated_films:
        await message.reply("<b>На жаль, немає фільмів з рейтингом для рекомендації.</b>")
        return

    # Сортуємо за рейтингом та беремо топ-3
    top_films = sorted(rated_films, key=lambda x: float(x['rating']), reverse=True)[:3]

    # Відправляємо інформацію про кожний рекомендований фільм
    await message.reply("<b>🍿 Best ⭐️ Films:</b>")

    for i, film_data in enumerate(top_films, 1):
        film = Film(**film_data)
        text = (f"<b>#{i} Рекомендований фільм:</b>\n"
                f"<b>Назва:</b> {film.name}\n"
                f"<b>Опис:</b> {film.description}\n"
                f"<b>Рейтинг:</b> ⭐️ {film.rating}/10\n"
                f"<b>Жанр:</b> {film.genre}\n"
                f"<b>Актори:</b> {', '.join(film.actors)}\n")

        await message.answer_photo(
            caption=text,
            photo=URLInputFile(
                film.poster,
                filename=f"{film.name}_poster.{film.poster.split('.')[-1]}"
            ),
            parse_mode="HTML"
        )


# Головна асинхронна функція для запуску бота
async def main() -> None:
    # Ініціалізуємо екземпляр бота з токеном та властивостями за замовчуванням
    bot = Bot(token=TOKEN, default=DefaultBotProperties(parse_mode=ParseMode.HTML))
    # Встановлюємо команди бота
    await bot.set_my_commands(BOT_COMMANDS)

    # Запускаємо цикл опитування для отримання оновлень
    await dp.start_polling(bot)


# Перевіряємо, чи скрипт запускається напряму
if __name__ == "__main__":
    # Налаштовуємо базове логування для виведення інформаційних повідомлень у стандарт`ний потік виведення
    logging.basicConfig(level=logging.INFO, stream=sys.stdout)
    # Запускаємо головну асинхронну функцію
    asyncio.run(main())
```

🧩 Необхідно запустити **TelegramBot**:

- Перевірити роботу програми.
- Звернути увагу на оновлений **вивід інформації** в **консоль**.
- Перевірити **записи** в **журналі** `logger_journal.log`

[Повернутися до змісту](#зміст-уроку)

---

## 6. Підведення підсумків 🚀

> На цьому уроці ми вивчили наступні теми:

- Як використовувати інструменти `print()` та  `pdb` для налагодження коду, що дозволяє швидко знайти і виправити
  помилки.
- Як налаштувати **логування** подій в **TelegramBot**, щоб зберігати інформацію про роботу програми та дії
  користувачів, що покращує підтримку та аналіз роботи програми.
- Розглянули базові методи тестування для перевірки функцій бота, що допомагає уникати помилок під час внесення змін у
  код.

> Сьогоднішній урок надає важливі навички, які дозволять вам створювати надійні та зручні у підтримці програми, а також
> підвищуючи якість вашого коду та покращуючи процес розробки.

[Повернутися до змісту](#зміст-уроку)

---
