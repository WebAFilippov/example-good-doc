[![latest](https://img.shields.io/github/v/release/GyverLibs/EncButton.svg?color=brightgreen)](https://github.com/GyverLibs/EncButton/releases/latest/download/EncButton.zip)
[![PIO](https://badges.registry.platformio.org/packages/gyverlibs/library/EncButton.svg)](https://registry.platformio.org/libraries/gyverlibs/EncButton)
[![Foo](https://img.shields.io/badge/Website-AlexGyver.ru-blue.svg?style=flat-square)](https://alexgyver.ru/)
[![Foo](https://img.shields.io/badge/%E2%82%BD%24%E2%82%AC%20%D0%9F%D0%BE%D0%B4%D0%B4%D0%B5%D1%80%D0%B6%D0%B0%D1%82%D1%8C-%D0%B0%D0%B2%D1%82%D0%BE%D1%80%D0%B0-orange.svg?style=flat-square)](https://alexgyver.ru/support_alex/)
[![Foo](https://img.shields.io/badge/README-ENGLISH-blueviolet.svg?style=flat-square)](https://github-com.translate.goog/GyverLibs/EncButton?_x_tr_sl=ru&_x_tr_tl=en)  

[![Foo](https://img.shields.io/badge/ПОДПИСАТЬСЯ-НА%20ОБНОВЛЕНИЯ-brightgreen.svg?style=social&logo=telegram&color=blue)](https://t.me/GyverLibs)

# EncButton

| ⚠️⚠️⚠️<br>**Новая версия v3 несовместима с предыдущими, смотри [документацию](#docs), [примеры](#example) и краткий [гайд по миграции](#migrate) с v2 на v3!**<br>⚠️⚠️⚠️ |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

Асинхронная библиотека для управления кнопкой и энкодером с Arduino
### Возможности
- Кнопка
  - Обработка событий: нажатие, отпускание, клик, количество кликов, удержание кнопки, импульсное удержание и время удержания. Также можно настроить предварительные клики для всех режимов.
  - Программное подавление дребезга (нежелательных повторных нажатий).
  - Возможность обрабатывать две одновременно нажатые кнопки как одну.
- Энкодер
  - Обработка событий: обычный поворот, нажатый поворот, быстрый поворот.
  - Поддержка четырёх типов инкрементальных энкодеров.
  - Высокоточный алгоритм определения положения.
  - Буферизация в прерывании (временная задержка для обработки данных).
    
### Особенности
- Жёсткая оптимизация и небольшой вес во Flash и SRAM памяти: 5 байт SRAM (на экземпляр) и ~350 байт Flash на обработку кнопки
- Максимально быстрое чтение пинов для AVR, esp8266, esp32 (используется GyverIO)
- Виртуальный режим (например для работы с расширителем пинов)

### Совместимость
Совместима со всеми Arduino платформами (используются Arduino-функции)

## Содержание
- [Установка](#install)
- [Информация](#info)
- [Документация](#docs)
  - [Настройки компиляции](#config)
  - [Полное описание классов](#class)
  - [Обработка и опрос](#tick)
  - [Предварительные клики](#preclicks)
  - [Прямое чтение кнопки](#btnread)
  - [Погружение в цикл](#loop)
  - [Timeout](#timeout)
  - [Busy](#busy)
  - [Получение события](#actions)
  - [Оптимизация](#optimise)
  - [Коллбэки](#callback)
  - [Одновременное нажатие](#double)
  - [Прерывания](#isr)
  - [Массив кнопок/энкодеров](#array)
  - [Кастомные функции](#custom)
  - [Опрос по таймеру](#timer)
  - [Мини примеры, сценарии](#examples-mini)
- [Миграция с v2](#migrate)
- [Примеры](#example)
- [Версии](#versions)
- [Баги и обратная связь](#feedback)

<details>
<summary>## Установка</summary>
Текст внутри спойлера.
</details>
