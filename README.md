<h1> Князева Анна, группа 4589 </h1>

<h3><i> Итоговая работа</i></h3>

**Операционные системы и виртуализация (Linux)**

1. Использование команды cat в Linux:
- Создать два текстовых файла: "Pets"(Домашние животные) и "Pack animals"(вьючные животные), используя команду cat в терминале Linux. В первом файле перечислить собак, кошек и хомяков. Во втором — лошадей, верблюдов и ослов.
- Объединить содержимое этих двух файлов в один и просмотреть его содержимое.
- Переименовать получившийся файл в "Human Friends".

```
gui@gb-linux:~/final_project$ cat > Pets
собаки
кошки
хомяки
gui@gb-linux:~/final_project$ cat > Pack_animals
лошади
верблюды
ослы
gui@gb-linux:~/final_project$ cat Pets Pack_animals > Animals
gui@gb-linux:~/final_project$ cat Animals
собаки
кошки
хомяки
лошади
верблюды
ослы
gui@gb-linux:~/final_project$ mv Animals Human_Friends
```
2. Работа с директориями Linux:
- Создать новую директорию и переместить туда файл "Human Friends".
```
gui@gb-linux:~/final_project$ mkdir animals
gui@gb-linux:~/final_project$ mv Human_Friends animals
gui@gb-linux:~/final_project$ cd animals/
gui@gb-linux:~/final_project/animals$ ll
итого 12
drwxrwxr-x 2 gui gui 4096 дек 7 21:45 ./
drwxrwxr-x 3 gui gui 4096 дек 7 21:45  ../
-rw-rw-r-- 1 gui gui   76 дек 7 21:27 Humal_Friends
```
3. Работа с MySQL в Linux. “Установить MySQL на вашу вычислительную машину ”
- Подключить дополнительный репозиторий MySQL и установить один из пакетов из этого репозитория.
