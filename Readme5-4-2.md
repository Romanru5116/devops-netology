* Задача 1
"Создайте собственный образ любой операционной системы (например, debian-11) с помощью Packer"
     - Начало работы с Packer
      - Подготовьте  облако к работе 
      - регистрация и вот это все сделано
      - установите CLI Yandex Cloud.
        curl -sSL https://storage.yandexcloud.net/yandexcloud-yc/install.sh | bash
      - Результат: готово: Yandex Cloud CLI 0.112.0 linux/amd64
      - Создание профиля
            -получите токен.
      - Выполнено
      - инициализируйте. 
      - Выполнено
      - кажется к работе облака готово

    + УСТАНОВИТЕ PACKER  
       - качаем архив с зеркала
       - распаковываем unzip (packer_версия_linux_amd64.zip
       - Переместить двоичный файл в каталог /usr/local/bin: 
       - установить PATH

    
       - создаю директорию для работы с пакером  md Packer
        - в ней создать VIM c конфигом:
    vim onfig.pkr.hcl
        - собственно установить плагин: packer init ~/devops-netology/packer/config.pkr.hcl
    Прошло время надо вспомнить:
       - смотрим что стоит тут вообще
       - Запрос: 
rrm@smart:~/devops-netology$ packer plugins installed
       - смотрим ответ: /home/rrm/.config/packer/plugins/github.com/hashicorp/yandex/packer-plugin-yandex_v1.1.2_x5.0_linux_amd64
    + Подготовьте конфигурацию образа

      1. Подготовьте конфигурацию образа : yc config list РЕЗУЛЬТАТ: 
      token: много_цифр
cloud-id: b1gu2ah0guc775lscaas
folder-id: b1gj0vu8t492kkqot4ua
compute-default-zone: ru-central1-a
r

      2. Подготовьте идентификатор подсети, выполнив команду yc vpc subnet list.
      Результат много букв и цифр: 
       default-ru-central1-a | enpg8g8877c8gfr70akh

      3.Создайте JSON-файл с любым именем, например, image1.json.
        + Запишите туда следующую конфигурацию:
        + сделано
        + Создайте образ
        + завершение с ошибкой
    "Builds finished but no artifacts were created"- Чиним - теперь успешно.
    Результат: ![образ готов](https://github.com/Romanru5116/devops-netology/blob/7c80a8b81dedc032356c8dcb30006eaadaf91009/image1_ok.png)

* Задача2
"Создайте вашу первую виртуальную машину в YandexCloud с помощью web-интерфейса YandexCloud."

![виртмашина]
(https://github.com/Romanru5116/devops-netology/blob/3fba18d710e7192404a06fcb40c2dfc8fbdbc219/VirtualMachine.png)

* ЗАДАЧА 3.1
 + создаем вирт машину из консоли взяли собственный образ DEBIAN - не описываю там все просто

 + на локальной машине складываем все файлы из ansible сюда же скидываем
provisionin.yml и правим его по факту (пользователь/ ssh/директория)
правим inventory - ip адрес машины из облака

указываем ansible  на местный inventory
ansible all --list-hosts -i inventory
видим есть

 + проверяем что ansible работает
ansible all -i inventory -m ping
 +[ping](https://github.com/Romanru5116/devops-netology/blob/14aaf83e33262ca0bcc445666acaf38458523834/ping.png)
 + теперь в рабочем режиме:
ansible-playbook provisionin.yml -i inventory
++ результат не тот

[Error](https://github.com/Romanru5116/devops-netology/blob/680290beef9fa002dfd56c8fc25ad4b475a53cf8/ErrorPlay.png)
++ 
+ надо переделывать под centos
виртуалку 24.10.23:30 пока здесь остановился
[NewCentos](https://github.com/Romanru5116/devops-netology/blob/0b60bfb70ed5b11aaf4c6576d16934b9e3b6df8e/newCentos.png)


++ продолжаем 26.10
++ машина на centos
++ правим инвентори
++ запускаем playbook - та же ошибка
гуглим и меняем строку запуска вот с этим: ansible-playbook -e ansible_python_interpreter=/usr/bin/python2

![питон надо развернутьудаленно сервере](/home/rrm/devops-netology/Img/errorpython.png)
  -заходим на сервер
смотрим версию python  --version
версия 2.7.5
  - вариант с развертыванием с 0
подключаем репозиторий epel
  - sudo yum install epel-release
  -далее сам python
  -sudo yum install python3 python3-devel python3-pip
  -проверяем:python3 -V версия 3.6.8

+ заново запускаем ansible

+ ошибка в задаче 2
![ScrERRTask2.png](/home/rrm/devops-netology/Img/ScrERRTask2.png)

+ сначала ставим сборку
sudo yum install libselinux-python3

+ далее ошибку с host
sudo yum install bind-utils

+ на облачном хосте проверил HOST- работает

+ 27.10 00:40 вновь на исполнение
плейбук
ошибка errorTools Installed
![errortools](/home/rrm/devops-netology/Img/errortaskInstalling.png)


+29.10 
+ "ручками создаем STACK и поддиректории"
* ЗАДАЧА 3.2
 + повторяем вышеописанные процедуры
приходим к успешному выполнению задач кроме единственной

 + ![timeout](/home/rrm/devops-netology/Img/prompt.png)
 + ИНТЕРНЕТ говорит что надо лечить правкой ansible.cfg - правим:
timeout=60

 + запускаем заново
 + ошибка:
![Питон2нужен](/home/rrm/devops-netology/Img/python2needed.png)
 + пробуем поставить версию2
sudo add-apt-repository universe
sudo apt update
sudo apt install python2

 + rrm@smart:~/devops-netology$ python2 --version
Python 2.7.18

+ гоним плейбук снова
и изменение строки запуска:
- ansible-playbook -e -ansible_python_interpreter=/usr/bin/-python2
+ ошибка нет директории STACK
ручками создаем STACK и поддиректории

+ опять запускаем ansible
выполнение успешно, результат
![ansibleok](/home/rrm/devops-netology/Img/screenWorkok.png)


* РЕЗУЛЬТАТ
![вирт машина](/home/rrm/devops-netology/Img/Virtual1.png)
![вирт машина](/home/rrm/devops-netology/Img/Virtual2.png)
![docker ps](/home/rrm/devops-netology/Img/docker_ps.png)

* ЗАДАЧА4
 + 1.Откройте веб-браузер: - вот так
![NotReach](/home/rrm/devops-netology/Img/NotReach.png)

 + Диагностика:
  - на удаленном пытаемся развернуть chrome
 - не запустился
 - ставим telnet
 - локально: telnet connect to address 127.0.0.1: Connection refused
 - проверяем как прокинут порт графаны из контейнера
 _видно что контейнер grafana слушает TCP порт 3000 
 задан вопрос в общую чатку около задачи- его как то надо прокинуть в контейнер? В каком конфиге править?_

 
Дополнительно по docker logs вижу что ошибки есть контейнеров:
"Есть ошибки по caddy 2023/10/29 19:56:19 loading Caddyfile via flag: open /etc/caddy/Caddyfile: no such file or directory"


