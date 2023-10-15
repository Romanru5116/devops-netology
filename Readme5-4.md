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
--сеть была, не было файлового хранилища
образ диска- сделал на диске из свежесозданного образа
![виртмашина]
(https://github.com/Romanru5116/devops-netology/blob/3fba18d710e7192404a06fcb40c2dfc8fbdbc219/VirtualMachine.png)
