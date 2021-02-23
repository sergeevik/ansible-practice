## Проект для тренировки ansible

Файл docker-compose.yml создает пачку образов на основе [Образа rastasheep/ubuntu-sshd](https://hub.docker.com/r/rastasheep/ubuntu-sshd)

1. Каждый образ открывает 22 порт, чтобы к нему можно было подключиться по ssh внутри сети
2. Образ ansible мапит localhost:22 на порт контейнера, чтобы можно было подключаться через ssh user@localhost
3. В каждом образе создает дефолтный пользователь root с паролем root
4. В каждом образе надо выполнить apt update, чтобы обновить все пакеты
5. Необходимо руками устанавливать нужные пакеты, образ ubuntu довольно пустой. 
    - Рекомендации к установке:
      - sudo `apt install sudo`
      - net-tool `apt install net-tool`
      - ping `apt install iputils-ping`
6. Чтобы узнать ip адреса контейнеров внутри сети надо снаружи (на своем компьютере, а не внутр образа) выполнить `docker inspect ansible_default` блок "Containers" атрибут "IPv4Address"
7. Создать нового пользователя командой (заменить username на желаемый логин в 2х местах): `useradd username -m -d /home/username -s /bin/bash -G sudo`
8. Установить для этого пользователя пароль кодманой: `passwd username`


## Что можно изменить в docker-compose.yml:
1. Имена образов первый уровень под services
2. Добавить открытые порты в тарибуте expose (для windows их надо обрачивать в ковычки)
3. Имя хочта, атрибут hostname, лучше если оно будет совпадать с именем образа в п.1
