### Модульное программирование на С ###

Модульное программирование — это организация программы как совокупности небольших независимых блоков, называемых 
модулями.

Модуль — функционально законченный фрагмент программы, оформленный в виде отдельного файла с исходным кодом. Модули 
проектируются таким образом, чтобы предоставлять программистам удобную для многократного использования функциональность 
(интерфейс) в виде набора функций, классов, констант. Модули могут объединяться в пакеты и, далее, в библиотеки. Удобство 
использования модульной архитектуры заключается в возможности обновления (замены) модуля, без необходимости изменения 
остальной системы.

Использование модульного программирования позволяет упростить тестирование программы и обнаружение ошибок. Модульность 
часто является средством упрощения задачи проектирования программы и распределения процесса разработки между группами 
разработчиков. При разбиении программы на модули для каждого модуля указывается реализуемая им функциональность, а также 
связи с другими модулями.

#### Выделение функций в модуль ####
Модуль в языке Си состоит из интерфейса (заголовочого файла **.h**) и реализации (файла **.c**).

Код, подключающий модуль, на этапе компиляции нуждается только в интерфейсе модуля, поэтому на этапе препроцессинга 
заголовочный файл копируется в код директивой `#include "somelib.h"`.

Реализация модуля должна полностью реализовывать указанный интерфейс, поэтому она также включает свой заголовочный файл.

Итого, пример проекта из основного файла и одного модуля, может выглядеть так:
```c
//main.c
#include <stdlib.h>
#include "hello.h"
int main()
{
    hello_world();
    return EXIT_SUCCESS;
}
```
```c
//hello.h
#ifndef HELLO_H
#define HELLO_H
void hello_world();
#endif //HELLO_H
```
```c
//hello.c
#include "hello.h"
#include <stdio.h>
void hello_world()
{
    printf("Hello, World!\n");
}
```

#### Замечание ####

В данном примере в файле **main.c** не понадобилось подключать **stdio.h**, хотя он и используется в модуле **hello.c**. Причина этого 
в том, что никакие типы из **stdio.h** не нужны для корректной обработки интерфейса **hello.h**, оказывающегося в **main.c** на этапе 
компиляции.

Если бы определения из какой-то библиотеки были необходимы для обработки интерфейса модуля, эти библиотеки должны были бы 
быть включены не в **hello.c**, а в **hello.h**, чтобы во всех местах, где подключается модуль hello, не возникало ошибок компиляции, 
так как эта библиотека автоматически подключена.
