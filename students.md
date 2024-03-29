---
layout: page
title: Темы проектов для курсовых/дипломов
---

## 1) A Redex-like framework for OCaml
  При создании и тестировании операционной семантики языка
  программирования крайне полезно иметь запускаемую модель,
  или интерпретатор, этой семантики.
  [PLT/Redex](https://redex.racket-lang.org/) является
  одним из самых удобных средств для разработки таких моделей.
  Этот framework разработан поверх диалекта LISP ---
  [Racket](https://racket-lang.org/). Как следствие, при
  работе с PLT/Redex приходится писать большое количество
  скобок (LISP!) и довольствоваться run-time проверкой типов.
    
  В рамках данного проекта предлагается разработать
  [DSL](https://en.wikipedia.org/wiki/Domain-specific_language)
  в OCaml ([camlp5](http://camlp5.gforge.inria.fr/)),
  обладающий схожей функциональностью, но имеющий
  преимущества языка с богатой системой типов, а также способный
  работать в браузере ([js_of_ocaml](http://ocsigen.org/js_of_ocaml/)).

## 2) An Operational Semantics for C/C++11 Concurrency and MiniKanren
  В 2011 стандарте C/C++ появилось описание семантики
  параллельных программ с data-races, или модель памяти.
  Она очень сложная и контринтуитивная. Однако она соответствует
  тому, как ведут себя параллельные программы на реальных процессорах
  после компиляции настоящими компиляторами.
  Также понимание этой модели необходимо для реализации параллельных
  lock-free алгоритмов на C/C++.

  [MiniKanren](http://minikanren.org/)
  --- это язык реляционного программирования. С помощью него
  можно писать обратимые функции. Например, по результату работы
  функции `append`, понять с какими аргументами она была вызвана.
  
  В рамках данного проекта мы используем MiniKanren, а точнее его
  [OCaml реализацию](https://github.com/dboulytchev/ocanren),
  для того, чтобы написать обратимый интерпретатор
  [операционной семантики языка с моделью памяти близкой C/C++11](https://podkopaev.net/opc11),
  что позволит нам по поведению программы получать её код. 
  
  Релевантная, но немножко устаревшая презентация проекта:
  [PDF](https://drive.google.com/open?id=0B3UPtzTx9FB1NGh0UlR2cWhNSWM).

## 3) Ostap, Kisa, and Sample-Based Formatting
  Создание синтаксических анализаторов и систем форматирования
  достаточно трудоёмко. Классическим подходом к решению этих задач
  в функциональном программировании являются библиотеки парсер- и
  принтер-комбинаторов. Например, библиотеки
  [ostap](https://github.com/dboulytchev/ostap) и
  [kisa](https://github.com/anlun/kisa).
  
  Также существует подход
  [форматирования по образцу](http://ntv.spbstu.ru/fulltext/T4.224.2015_04.PDF) (ФO),
  который позволяет пользователю отформатировать целевой код в соответствии
  со стилем некоторого проекта без ручного задания десятков настроек форматирования
  (как это происходит в современных IDE), а просто передав системе эталонный проект.
  
  В рамках данной темы планируется провести слияние ФО
  и способа задания парсер-комбинаторов в виде грамматики, как в
  [ostap](https://github.com/dboulytchev/ostap), и реализовать это
  всё как [DSL](https://en.wikipedia.org/wiki/Domain-specific_language)
  в OCaml ([camlp5](http://camlp5.gforge.inria.fr/)),
  Это позволит по грамматикам получать не только парсер, как это происходит сейчас,
  но и принтер, обладающий выразительностью ФО.

