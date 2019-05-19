# Сервис дискреционного управления доступом, 
## Описание:
Сервис выполняет мониторинг прав доступа наиболее важных системных конфигурационных файлов раз в минуту. В случае отклонения прав доступа, сервис изменяет права доступа на стандартные. Список файлов для мониторинга располагается в конфигурационном файле. Сервис работает в режиме системной службы и ведет собственный журнал событий.

## Cлужебные файлы (располагаются в /opt/checker/):   

Название файла  | Описание файла
----------------|----------------------
checker.conf    | конфигурационный файл, хранит список файлов, права доступа к которому мониторятся сервисом
checker.service | юнит  
checker.pid     | создается в ходе работы сервиса, хранит pid процесса, по которому контролируется работоспособность сервиса: перезапуск сервиса в случае прекращения его работы
checker.sh      | код программы 
checker.repo    | конфигурационный файл для подключения репозитория

## Запуск сервиса:
Кладем checker.service в /etc/systemd/system  
Смотрим его статус: **systemctl status checker**  
  
Видим, что он disabled — разрешаем его:  
**systemctl enable checker**  
**systemctl -l status checker**

Запускаем сервис: **systemctl start checker**  
Смотрим статус:  **systemctl -l status checker**  

Если что-то пошло не так, перезагружаем демон: **systemctl daemon-reload**  

## Подключение репозитория к системе
Для подключения репозитория необходимо поместить файл **checker.repo** по пути **/etc/yum.repos.d/checker.repo**
**centos.gremlinlab.com** - доменное имя сервера, содержащего репозиторий
**RPM-GPG-KEY-Pavel-Parkhomets** - публичный ключ одного из разработчиков, необходимый для проверки цифровой подписи.

Для установки пакета **chacker** после добавления репозитория используйте команду
**yum install checker**



## Разработчики:
- Максимова Анна (MaxiAnn)
- Сидорова  Анна (AnnaSidorovaMEPHI, annalouise, root) :D
- Кондратьев Дмитрий (dimaelf)
- Кооритс Виктор (VKoorits)
- Пархомец Павел (gremlin)


