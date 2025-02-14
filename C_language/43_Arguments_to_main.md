### Аргументы функции main() ###

Иногда при запуске программы бывает полезно передать ей какую-либо информацию. Обычно такая информация передается 
функции **main()** с помощью аргументов командной строки. *Аргумент командной строки* — это информация, которая вводится 
в командной строке операционной системы вслед за именем программы.

Чтобы принять аргументы командной строки, используются два специальных встроенных аргумента: **argc** и **argv**. Параметр 
**argc** содержит количество аргументов в командной строке и является целым числом, причем он всегда не меньше **1**, потому 
что первым аргументом считается имя программы. А параметр **argv** является указателем на массив указателей на строки. 
В этом массиве каждый элемент указывает на какой-либо аргумент командной строки. Все аргументы командной строки 
являются строковыми, поэтому преобразование каких бы то ни было чисел в нужный двоичный формат должно быть предусмотрено 
в программе при ее разработке.

Вот простой пример использования аргумента командной строки. На экран выводятся слово **Привет** и ваше имя, которое надо 
указать в виде аргумента командной строки.
```c
#include <stdio.h>
#include <stdlib.h>
int main(int argc, char *argv[])
{
  if(argc!=2) {
    printf("Вы забыли ввести свое имя.\n");
    exit(1);
  }
  printf("Привет %s", argv[1]);
  return 0;
}
```
Если вы назвали эту программу `name` (имя) и ваше имя Том, то для запуска программы следует в командную строку ввести `name Том`. 
В результате выполнения программы на экране появится сообщение

Привет, Том.

Во многих средах все аргументы командной строки необходимо отделять друг от друга пробелом или табуляцией. Запятые, 
точки с запятой и тому подобные символы разделителями не считаются. Например,
```c
run Spot, run
```
состоит из трех символьных строк, в то время как
```c
Эрик,Рик,Фред
```
представляет собой одну символьную строку — запятые разделителями не считаются.

Если в строке имеются пробелы, то, чтобы из нее не получилось несколько аргументов, в некоторых средах эту строку 
можно заключать в двойные кавычки. В результате вся строка будет считаться одним аргументом. Чтобы подробнее узнать, 
как в вашей операционной системе задаются параметры командной строки, изучите документацию этой системы.

Очень важно правильно объявлять  argv:
```c
char *argv[];
```
Пустые квадратные скобки указывают на то, что у массива неопределенная длина. Теперь получить доступ к отдельным 
аргументам можно с помощью индексации массива `argv`. Например, `argv[0]` указывает на первую символьную строку, которой всегда является 
имя программы; `argv[1]` указывает на первый аргумент и так далее.
