# Заметки о функциональном и логическом программировании

[[Перейти к оглавлению](README.md)]

## Статическая и динамическая типизация

*Статическая типизация* означает то, что типы объектов программы известны до
того, как программа будет запущена. *Динамическая типизация* по сути
противоположна статической и означает, что типы определяются во время
выполнения программы. У обоих видов типизации есть как преимущества, так и
недостатки.

### Статическая типизация

Преимущества статической типизации:

- Появляется возможность компиляции в непосредственно исполняемый машинный код.

- Появляется возможность как высокоуровневой, так и низкоуровневой оптимизации
исполняемого кода.

- Компилятор способен выловить не только синтаксические ошибки, но и логические,
связанные с несоответствием типов.

- Облегчается реализация функции автодополнения в редакторах кода для языков со
статической типизацией. Интересно, например, что автодополнение для
динамически типизированного JavaScript в среде Visual Studio Code реализовано
через посредство определений типов для TypeScript.

- Самодокументирование кода. При явном указании типов легко разобраться,
например, что подаётся на вход функции, и что эта функция должна вернуть.

- Уменьшается объём тестов, так как отпадает целый класс тестов, например,
связанных с проверкой входных данных на соответствие типов. Есть расхожее
мнение, что если программу на языке Haskell наконец удалось скомпилировать, то
скорее всего она будет работать правильно. В случае Haskell и родственных языков
практика показывает, что это действительно так. Ситуация с языками с зависимыми
типами (Idris, Agda) ещё лучше. В этих языках реализована возможность
доказательства программ, что практически сводит на нет необходимость писать
тесты.

Недостатки статической типизации:

- Для некоторых языков характерна многословность, связанная с необходимостью
задавать типы для всех объектов программы, например, в C# и Java. Ещё сравни,
например, код программ на Visual Prolog и SWI Prolog. Однако, во многих
современных языках есть вывод типов, позволяющий во многих ситуациях не
задавать тип. Тип в этом случае будет вычисляться самим компилятором. В
современных C# и C++ есть возможность не указывать явно тип определяемой
переменной. В C# для этого есть ключевое слово var, а в C++ auto. В Haskell
и языках семейства ML имеется полноценный механизм вывода типов.

- Требуется явный этап компиляции и сборки программы перед её запуском. Этот
этап может занимать много времени даже при небольших изменениях в коде.

- Статическое связывание, затрудняющее горячую замену кода. Фактически горячая
замена возможна только на уровне отдельных программных процессов.

- Сложно работать со слабоструктурированными данными, например, данными в
формате JSON, структура которых может меняться и допускать пробелы.

Языки со статической типизацией: C, C++, Pascal, Fortran, C#, Java, TypeScript,
Flow, Standard ML, Haskell, Elm, Idris, Agda, Scala, OCaml, F#, Rust,
Visual Prolog.

### Динамическая типизация

Преимущества динамической типизации:

- В теории более лаконичный код, так как отпадает обязанность по объявлению
типов объектов программ, однако на практике код на динамически типизированных
языках ради обеспечения большей надёжности наполовину состоит из проверок
на соответствие типов.

- Возможна интерпретация кода. Но опять же, в реальности многие языки с
динамической типизацией слишком сложны, чтобы выполнять код построчно, поэтому
обычно присутствует скрытый этап компиляции кода в промежуточное представление
или в код виртуальной машины. При этом трудно назвать языки, которые бы
позволяли компиляцию в непосредственно исполняемый машинный код, в отличие от
языков со статической типизацией.

- Широко распространено динамическое связывание, открывающее двери для горячей
замены кода. К числу таких языков можно отнести Erlang, Lisp и Smalltalk.
Стоит обратить внимание на то, что ни один из этих трёх языков не является
широко распространённым.

- Возможность на лету изменять структуру и тип объектов позволяет легко
обрабатывать слабоструктурированные данные, например, в формате JSON. Более
того, формат JSON потому и прижился и стал, наверное, самым популярным благодаря
прозрачной интеграции с JavaScript, самым популярным языком для веб-разработки.

Недостатки динамической типизации:

- Невозможно реализовать компиляцию в эффективный машинный код, так или иначе
потребуется код времени исполнения для обслуживания динамической природы
объектов.

- Оптимизация кода затруднительна по разным причинам.

- Синтаксические ошибки вылавливаются большинством языков до того как программа
заработает, однако многие типичные ошибки на этом этапе не вылавливаются,
например, в Python можно сделать опечатку в имени переменной и компилятор этого
не заметит, так как явного объявления имён переменных здесь нет. И это
характерная ситуация для большинства динамически типизированных языков. Частично
облегчает ситуацию использование специальных утилит под названием linter,
которые проверяют код на возможные ошибки, в том числи связанные с типами и с
использованием имён.

- Так как тип объекта может быть любой, то качественно реализовать в редакторах
кода поддержку автодополнения не представляется возможным.

- Ограниченное самодокументирование кода. Характерно широкое использование
так называемых аннотаций, облегчающих как документирование, так и
автодополнение. Однако аннотации не являются частью синтаксиса языка и
компиляторами обычно игнорируются.

- Для поддержания качества разработки программ требуется писать большое
количество тестов, в число которых входят тесты на проверку несоответствия
типов.

- Ограниченная перегрузка подпрограмм. Возможна, и то не всегда, по количеству
входных параметров, но не по их типу.

Языки с динамической типизацией: Python, PHP, Ruby, Perl, JavaScript, Erlang,
Lisp, SWI Prolog.

## Источники

- [Статическая типизация (статья в Википедии)](https://ru.wikipedia.org/wiki/Статическая_типизация)

- [Динамическая типизация (статья в Википедии)](https://ru.wikipedia.org/wiki/Динамическая_типизация)

- [Статическая и динамическая типизация (статья на Хабрахабре)](https://habrahabr.ru/post/308484/)

- [Горячая замена](https://ru.wikipedia.org/wiki/Горячая_замена)

- [Горячая замена кода (блог Ивана Блинкова)](https://www.insight-it.ru/theory/2013/goryachaya-zamena-koda/)

- [Десять причин не использовать статически типизированный функциональный язык программирования](https://habrahabr.ru/post/190492/)

[[Перейти к оглавлению](README.md)]

---

&copy; [Евгений А. Симоненко](LICENSE.md), 2017
