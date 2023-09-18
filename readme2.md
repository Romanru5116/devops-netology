

# Практическая работа

`style`: List style (`string`, default `consistent`, values `asterisk` /
  `consistent` / `dash` / `plus` / `sublist`)

 "Домашнее задание к занятию 2. «Применение принципов IaaC в работе с виртуальными машинами»"

Ответы на вопросы

* Задача 1

  * Вопрос1:"Опишите основные преимущества применения на практике IaaC-паттернов."
  * Ответ1: 
  * 1.Быстрое получение инфраструктуры требуемой   конфигурации.
    2.Процесс создания и настройки аналогичен процессу разработки ПО. 
  3. Предположительно - невысокий Т.С.О.(стоимость владения).

* ВОПРОС2.Какой из принципов IaaC является основополагающим?
* ОТВЕТ: Идемпотентность- свойство объекта или операции при повтором выполнени дающее тот же самый результат.

* Задача 2

* ВОПРОС:Чем Ansible выгодно отличается от других систем управление конфигурациями?

+ ОТВЕТ: не требует установки доп агентов на управляемые сервера, быстрый вход, нативный для линукс систем
  +ВОПРОС: Какой, на ваш взгляд, метод работы систем конфигурации более надёжный — push или pull?
  +ОТВЕТ: Представляется что PUSH - понятно  что отправляешь в какой момент времени и можно обрабатывать ошибки.

* Задача 3
  + Установите на личный
 компьютер:
VIRTUALBOX

- как:надо узнать версию

 Ubuntu  lsb_release -a
(у меня 22.04)
+ с сайта скачать пакет

* получена ошибка- ядро не той версии

   + забороть ее пересборкой ядра

  + вывод версии:
"Oracle VM VirtualBox VM Selector v7.0.10
Copyright (C) 2005-2023 Oracle and/or its affiliates"
    
* VAGRANT
- скачать с офф сайта не доступно, лезем по предложенной ссылке, качаем нечто по ссылке с github

    - rrm@smart:~$ vagrant -v
    - Vagrant 2.3.7
* TERRAFORM

  + Шаг 1. Обновить список пакетов sudo apt update:
  + Шаг2 Установить нужную версию
  + попытка пойти "правильно из оригинального облака"неудачна
  + ЗАПРОС:rrm@smart:~/devops-netology/terraform$ wget https://releases.hashicorp.com/terraform/1.5.7/terraform_1.5.7x_linux_amd64.zip
--2023-09-17 12:06:21--  https://releases.hashicorp.com/terraform/1.5.7/terraform_1.5.7x_linux_amd64.zip
Resolving releases.hashicorp.com (releases.hashicorp.com)... 18.165.140.5, 18.165.140.50, 18.165.140.83, ...
Connecting to releases.hashicorp.com (releases.hashicorp.com)|18.165.140.5|:443... connected.
HTTP request sent, awaiting response... 404 Not Found
  + РЕЗУЛЬТАТ: 2023-09-17 12:06:22 ERROR 404: Not Found.

Шаг3:
Идем по ссылкам из задаания качаем с какого-то НЕПОНЯТНОГО  сайта НЕПОНЯТНЫЙ СОФТ стабильной версии  с названнием похожим на нужное:
 wget https://hashicorp-releases.yandexcloud.net/terraform/1.5.7/terraform_1.5.7_linux_amd64.zip

    ШАг4:делаем unzip

    Шаг5. Переместить в папку Переместите распакованный файл в папку /usr/local/bin

Шаг6 нужно почистить папку от установочного мусора
но есть не пойми что

    -rwxr-xr-x 1 rrm rrm 65200128 сен 17 01:14 terrafom*

Шаг 7. Проверьте версию Terraform и убедитесь, что он установлен и доступен: 
ДЕЛАЕМ: terraform -v
РЕЗУЛЬТАТ: 
Terraform v1.5.7
on linux_amd64

Шаг8 надо создать папку для конфигов
Создайте новую директорию с произвольным названием, например cloud-terraform.
У меня mtune.tf

Шаг 9 сконфигурить на какое то облако:- создать провайдера: в домашней директории y создать nano ~/.terraformrc и в него разместить provider_installation {
  network_mirror {
    url = "https://terraform-mirror.yandexcloud.net/"
    include = ["registry.terraform.io/*/*"]
  }
  direct {
    exclude = ["registry.terraform.io/*/*"]
  }
}

Шаг10:
правка конфига файла конфигурации


* ANSIBLE
 + 1.развернуть локально машину управления
 обновить пакеты
  - sudo apt-get update
  - sudo apt-get upgrade 

+ 2.развернуть ansible
 - sudo apt install ansible
- Ответ: ansible is already the newest version (2.10.7+merged+base+2.10.8+dfsg-1)

* Шаг 2 — Настройка файла инвентаризации


* Задача 4 "Воспроизведите практическую часть лекции самостоятельно"
Создайте виртуальную машину.
 ошибка системы "имя_некорректно" зарегистрирован тикет KL503985, исправил сам

  + вирт машина создана
file:///home/rrm/Pictures/Screenshots/virtMachine.png
  +зайти про докер посмотреть
результат "Command 'docker' not found, but can be installed with:"

+поставим докер: sudo apt install docker.io

