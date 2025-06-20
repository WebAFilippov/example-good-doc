[![latest](https://img.shields.io/github/v/release/GyverLibs/EncButton.svg?color=brightgreen)](https://github.com/GyverLibs/EncButton/releases/latest/download/EncButton.zip)
[![PIO](https://badges.registry.platformio.org/packages/gyverlibs/library/EncButton.svg)](https://registry.platformio.org/libraries/gyverlibs/EncButton)
[![Foo](https://img.shields.io/badge/Website-AlexGyver.ru-blue.svg?style=flat-square)](https://alexgyver.ru/)
[![Foo](https://img.shields.io/badge/%E2%82%BD%24%E2%82%AC%20%D0%9F%D0%BE%D0%B4%D0%B4%D0%B5%D1%80%D0%B6%D0%B0%D1%82%D1%8C-%D0%B0%D0%B2%D1%82%D0%BE%D1%80%D0%B0-orange.svg?style=flat-square)](https://alexgyver.ru/support_alex/)
[![Foo](https://img.shields.io/badge/README-ENGLISH-blueviolet.svg?style=flat-square)](https://github-com.translate.goog/GyverLibs/EncButton?_x_tr_sl=ru&_x_tr_tl=en)  

[![Foo](https://img.shields.io/badge/ПОДПИСАТЬСЯ-НА%20ОБНОВЛЕНИЯ-brightgreen.svg?style=social&logo=telegram&color=blue)](https://t.me/GyverLibs)


<h1 align="center" style="font-size: 2.5em; font-weight: bold; margin: 1em 0;">
  EncButton 3
</h1>
<p align="center"><em>Асинхронная библиотека для управления кнопкой и энкодером с Arduino</em></p>

---

> [!IMPORTANT]
> __Новая версия несовместима с предыдущими, смотри [документацию](#docs), [примеры](#example) и краткий [гайд по миграции](#migrate) с v2 на v3!__


# Содержание(#contents)

- [О программе](#about)
- [Установка](#install)
- [Документация](#doc)
  - [Концепция](#concept)
  - [Настройка](#settings)
  - [Методы](#methods)
    - [Concept](#conteps)
    - [Method1](#method-1)
    - [Method2](#method-2)
- [Использование](#using)
- [Техническая документация и сборка](#tech-info)

# 1. [О программе](#about)

## Возможности
#### Кнопка
  - Обработка событий: нажатие, отпускание, клик, количество кликов, удержание кнопки, импульсное удержание и время удержания. Также можно настроить предварительные клики для всех режимов.
  - Программное подавление дребезга (нежелательных повторных нажатий).
  - Возможность обрабатывать две одновременно нажатые кнопки как одну.
#### Енкодер
  - Обработка событий: обычный поворот, нажатый поворот, быстрый поворот.
  - Поддержка четырёх типов инкрементальных энкодеров.
  - Высокоточный алгоритм определения положения.
  - Буферизация в прерывании (временная задержка для обработки данных).

## Особенности
- Жёсткая оптимизация и небольшой вес во Flash и SRAM памяти: 5 байт SRAM (на экземпляр) и ~350 байт Flash на обработку кнопки
- Максимально быстрое чтение пинов для AVR, esp8266, esp32 (используется GyverIO)
- Виртуальный режим (например для работы с расширителем пинов)

## Совместимость
Совместима со всеми Arduino платформами (используются Arduino-функции)
<p align="right"><a href="#contents">К содержанию</a></p>

# 2. [Установка](#install)

> [!TIP]
> Для работы требуется библиотека [GyverIO](https://github.com/GyverLibs/GyverIO)

### Автоматическая установка
- Установите __EncButton__ через менеджер библиотек Arduino IDE, Arduino IDE v2 или PlatformIO.
### Ручная установка
- Для ручной установки: [Скачать библиотеку](https://github.com/GyverLibs/EncButton/archive/refs/heads/main.zip) и распаковать в:  
  - Windows x64: C:\Program Files (x86)\Arduino\libraries
  - Windows x32: C:\Program Files\Arduino\libraries
  - Документы/Arduino/libraries/
  - (Arduino IDE) автоматическая установка из .zip: Скетч/Подключить библиотеку/Добавить .ZIP библиотеку… и указать скачанный архив

> Подробная инструкция по установке библиотек доступна [по этой ссылке](https://alexgyver.ru/arduino-first/#%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_%D0%B1%D0%B8%D0%B1%D0%BB%D0%B8%D0%BE%D1%82%D0%B5%D0%BA).

### Обновление
- _Менеджер библиотек:_ найдите и нажмите "Обновить".
- _Вручную:_ удалите старую версию и замените новой, избегая замены файлов.

<p align="right"><a href="#contents">К содержанию</a></p>

# 3. [Документация](#doc)

В этой главе мы расскажем...

<details>
  <summary><a href="concept"><h3>Концепция</h3></a></summary>
  Описание классов

  <p align="right"><a href="#doc">К документации</a></p>
  <p align="right"><a href="#contents">К содержанию</a></p>
</details>

<details>
  <summary><a href="settings"><h3>Настройка</h3></a></summary>
  Объявлять до подключения библиотеки  

  ```cpp
  // отключить поддержку pressFor/holdFor/stepFor и счётчик степов (экономит 2 байта оперативки)
  #define EB_NO_FOR

  // отключить обработчик событий attach (экономит 2 байта оперативки)
  #define EB_NO_CALLBACK

  // отключить счётчик энкодера [VirtEncoder, Encoder, EncButton] (экономит 4 байта оперативки)
  #define EB_NO_COUNTER

  // отключить буферизацию энкодера (экономит 2 байта оперативки)
  #define EB_NO_BUFFER

  /*
    Настройка таймаутов для всех классов
    - Заменяет таймауты константами, изменить их из программы (SetXxxTimeout()) будет нельзя
    - Настройка влияет на все объявленные в программе кнопки/энкодеры
    - Экономит 1 байт оперативки на объект за каждый таймаут
    - Показаны значения по умолчанию в мс
    - Значения не ограничены 4000мс, как при установке из программы (SetXxxTimeout())
  */
  #define EB_DEB_TIME 50      // таймаут гашения дребезга кнопки (кнопка)
  #define EB_CLICK_TIME 500   // таймаут ожидания кликов (кнопка)
  #define EB_HOLD_TIME 600    // таймаут удержания (кнопка)
  #define EB_STEP_TIME 200    // таймаут импульсного удержания (кнопка)
  #define EB_FAST_TIME 30     // таймаут быстрого поворота (энкодер)
  #define EB_TOUT_TIME 1000   // таймаут действия (кнопка и энкодер)
  ```

  <p align="right"><a href="#doc">К документации</a></p>
  <p align="right"><a href="#contents">К содержанию</a></p>
</details>

<details>
  <summary><a href="methods"><h3>Методы</h3></a></summary>

  - [tick](#method-tick)
  - [setHoldTimeout](#method-setHoldTimeout)
  - setStepTimeout
  - setDebTimeout
  - setBtnLevel
  - setClickTimeout
  - tick
  - tickRaw
  - read
  - readBtn

  ### [tick()](#method-tick)

  __Описание:__ Основной метод для опроса состояния кнопки или энкодера. Должен вызываться в цикле →loop() для обработки событий (нажатий, вращений и т.д.). Для виртуальных классов принимает входные значения напрямую.

  ### [setHoldTimeout()](#method-setHoldTimeout)

  <p align="right"><a href="#doc">К документации</a></p>
  <p align="right"><a href="#contents">К содержанию</a></p>
</details>






