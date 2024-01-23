# Подготовка 

Для начала была создана вирутальная машина с помощью Oracle VM VirtuslBox.

![image](https://github.com/cs-itmo-2023/lab-4-Nirolok/assets/40453222/2f09319b-a84f-4711-bc54-1d67eeb9ff5c)

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

![огонёк и статус контенейра](https://github.com/cs-itmo-2023/lab-4-Nirolok/assets/40453222/aa5eed84-1429-4ee7-a72e-b0c3ece729ad)

Далее, с помощью команды `docker network create myNetwork`, создаём сеть, к которой подключим наши контейнеры.
Для подключения контейнеров нам понадобятся имена, которые можно узнать с помощью команды `docker ps` (столбец NAMES соотвентсвенно).

![Снимок экрана 2024-01-22 200910](https://github.com/cs-itmo-2023/lab-4-Nirolok/assets/40453222/099d237c-c78e-4417-b018-796766672ce6)

Затем используя команду `docker network inspect myNetwork` смотрим сведенья о нашей сети

![Снимок экрана 2024-01-22 200940](https://github.com/cs-itmo-2023/lab-4-Nirolok/assets/40453222/c70fe129-03f5-41df-9535-9f8983892a63)

С помощью `docker exec -it <id-нашего-контейнера> bash` открываем контейнеры и пингуем их чтобы проверить соеденение и убедиться в том, что всё работает.
![Снимок экрана 2024-01-22 201519](https://github.com/cs-itmo-2023/lab-4-Nirolok/assets/40453222/445eb9f8-1c5c-4984-ad1d-4efc96f9edd6)

На этом работу можно считать выполненой.
