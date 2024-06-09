# ZFS
## Создаем виртуальную машину
1. vagrant up
2. vagrant ssh
3. sudo -i

### Определение алгоритма с наилучшим сжатием
'''
1. Смотрим список всех дисков, которые есть в виртуальной машине: lsblk
2. Создаём пул из двух дисков в режиме RAID 1 (скрин 1)
3. Создадим ещё 3 пула (скрин 1)
4. Смотрим информацию о пулах (скрин 1, скрин 2)
5. Добавим разные алгоритмы сжатия в каждую файловую систему и проверим, что все файловые системы имеют разные методы сжатия (скрин 3)
6. Скачаем один и тот же текстовый файл во все пулы: 
[root@zfs ~]# for i in {1..4}; do wget -P /otus$i https://gutenberg.org/cache/epub/2600/pg2600.converter.log; done  (скрин 4)
    6.1  Алгоритм gzip-9 самый эффективный по сжатию (скрин 5)
'''
### Определение настроек пула
'''
1. Скачиваем архив в домашний каталог: 
[root@zfs ~]# wget -O archive.tar.gz --no-check-certificate 'https://drive.usercontent.google.com/download?id=1MvrcEp-WgAQe57aDEzxSRalPAwbNN1Bb&export=download' 
2. Разархивируем его: [root@zfs ~]# tar -xzvf archive.tar.gz
3. zpool import -d zpoolexport/ вывод показывает нам имя пула, тип raid и его состав (скрин 6)
4. Импорт данного пула к нам в ОС zpool import -d zpoolexport/ otus (скрин 7)
5. Запрос сразу всех параметром файловой системы: zfs get all otus
6. C помощью команд можно уточнить конкретный параметр (скрин 8)
'''
### Работа со снапшотом, поиск сообщения от преподавателя
'''
1. Скачаем файл, указанный в задании:
[root@zfs ~]# wget -O otus_task2.file --no-check-certificate https://drive.usercontent.google.com/download?id=1wgxjih8YZ-cqLqaZVa0lA3h3Y029c3oI&export=download
2. Восстановим файловую систему из снапшота:
zfs receive otus/test@today < otus_task2.file
3. Ищем в каталоге /otus/test файл с именем “secret_message” (скрин 9)
 3.1 Содержимое найденного файла - ссылка на курс
'''


