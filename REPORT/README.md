# Подготовка 

Для начала была создана вирутальная машина с помощью Oracle VM VirtuslBox.

![image](https://github.com/Nirolok/Laba_4/assets/40453222/29bf0fa4-6de0-4a11-bcfb-597b3f63afa7)


На данную машину,с помщью команды `sudo apt install curl`, устанавливаем curl, затем c помощью команды `curl -fsSl://get.docker.com -o get-docker.sh` устанавливаем скрипт, а после его установки,
запускаем командой `sudo sh get-docker.sh`, что в свою очередь загружает Docker.

# Реализация

После всех манипуляций создаём Dockerfile, в который включим aafire и ping:

(код, который необходимо прописать в Dockerfile)
~~~
FROM ubuntu:latest
RUN apt-get update && apt-get install -y libaa-bin
CMD ["aafire"]
RUN apt-get update && apt-get install -y iputils-ping
~~~

После чего необходимо прописать команды `docker build -t aafire .` и `docker run -it aafire`, для сборки и запуска контенера соответсвенно. 

В итоге получается ~~огнище~~ огонёк

![image](https://github.com/Nirolok/Laba_4/assets/40453222/7f5a7de5-9ccf-4353-9b1f-bd4e79a6b61b)


Далее, с помощью команды `docker network create myNetwork`, создаём сеть, к которой подключим наши контейнеры.
Для подключения контейнеров нам понадобятся имена, которые можно узнать с помощью команды `docker ps` (столбец NAMES соотвентсвенно).

![image](https://github.com/Nirolok/Laba_4/assets/40453222/1857f1ea-a006-4bc5-8b9d-1a3d31c5e8aa)


Затем используя команду `docker network inspect myNetwork` смотрим сведенья о нашей сети

![image](https://github.com/Nirolok/Laba_4/assets/40453222/45bfadd5-922c-4a3d-bf8a-ed9ec1749708)


С помощью `docker exec -it <id-нашего-контейнера> bash` открываем контейнеры и пингуем их чтобы проверить соеденение и убедиться в том, что всё работает.

![image](https://github.com/Nirolok/Laba_4/assets/40453222/df236d67-00f4-43e4-ae19-fb43c802d3af)


На этом работу можно считать выполненой.
