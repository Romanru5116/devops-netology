# Практическая работа 5-3
*Задача1

+ создать репозиторий
Результат:
![результат](/home/rrm/devops-netology/RepoDockerCreate.png)
+ выберите любой образ, который содержит веб-сервер Nginx;
![результат](/home/rrm/devops-netology/chooseImage.png)


* грусть с перестановкой docker
 и тут приходит понимание что развернут docker неправильно
- разворачиваем правильно
  - apt get update
- sudo apt install curl software-properties-common ca-certificates apt-transport-https 
-curl -f -s -S -L https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
 добавили репозиторий
 sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu jammy stable"
 установка из нужного репозитория
 apt-cache policy docker-ce
 Устанавливаем докер
sudo apt install docker-ce -y
успешная установка
sudo systemctl status docker
+ запуск без sudo неуспешен исправляем
+ sudo chown rrm:docker /var/run/docker.soc

+ создайте свой fork образа;
- создаем директорию для размещения mkdir -p /opt/docker/mynginx
- cd /opt/docker/mynginx
  - docker pull nginxinc/nginx-unprivileged
  ![результат](/home/rrm/devops-netology/dockerpull2.png)
  - отправим его же и обратно и считаем это заготовкой fork
  - куда это он закинул  
  docker info
  -Storage Driver: overlay2
  но нам нужно понять что с контейнером: docker inspect nginxinc/nginx-unprivileged

  - чтобы изменить файлы конфига надо корректно подготовить 
  длинный путь: отдельно папка для http и отдельно для картинок
  /data/www и data/images
  - смотрим какие есть images
  надо имя контейнера оттуда
  далее запустим контейнер:
  перейти в директорию где он хранится /opt/docker/mynginx$
запускаем в обычном режиме- плохо

![Ответ](/home/rrm/devops-netology/runit.png)

  -глубокая ночь 27-28,прервемся
  - продолжение 28
  -Задачка: вернуться к исходному состоянию docker и окружения
    - пойти в директорию где image, 
    в нашем случае rrm@smart:/opt/docker/mynginx$ 
    - там смотрим контейнеры и лишние остатки экспериментов прибиваем docker rm ID
    ![Ответ](/home/rrm/devops-netology/image_show.png)

    Теперь пытаемся использовать  
    - Метод 2: изменение образа с помощью фиксации докера
    - запустим nginxinc/nginx-unprivileged 

 docker run -it nginxinc/nginx-unprivileged sh

![проблема](/home/rrm/devops-netology/RunDocker.png)
проблема: порт не слушает, значит рубимdocker stop $(docker ps -a -q) и заново запускаем
docker run --name 3b18365df831 p 80:80 nginxinc/nginx-unprivileged


![проблема_решена,но нет IP](/home/rrm/devops-netology/listenRadio.png)

---здесь пока все что успел----

* ЗАДАЧА 2
+ вопрос выберите что подходит лучше:
 -Ответ: честно:  опыта проектирования нет, предполагать нет смысла, но кажется в случаях монолитных приложений все эти виртуализации просто не имеют смысла т.к. это скорее какое то решение в виде "супового набора" исполняемых файлов,  толстых клиентов, объектов .Net, "размазанной" между сервером бизнес приложений и БД функциональностью. 
виртуализацию имеет к.м.к. использовать когда часто менятся части приложений, а физические сервера всегда выигрывают в производительности, ибо процессору нет необходимости отрабатывать паразитный с т.зр. эффективности работы код виртуализации. Вопросы скорее в необходимости и стоимости кластеризации - аппаратной или программной. 

* ЗАДАЧА 3, 4 еще в процессе
