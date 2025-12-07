# Домашнее задание к занятию «Введение в Terraform»

### Цели задания

1. Установить и настроить Terrafrom.
2. Научиться использовать готовый код.

------

### Чек-лист готовности к домашнему заданию

1. Скачайте и установите **Terraform** версии >=1.12.0 . Приложите скриншот вывода команды ```terraform --version```.
2. Скачайте на свой ПК этот git-репозиторий. Исходный код для выполнения задания расположен в директории **01/src**.
3. Убедитесь, что в вашей ОС установлен docker.

------

### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. Репозиторий с ссылкой на зеркало для установки и настройки Terraform: [ссылка](https://github.com/netology-code/devops-materials).
2. Установка docker: [ссылка](https://docs.docker.com/engine/install/ubuntu/).
------
### Внимание!! Обязательно предоставляем на проверку получившийся код в виде ссылки на ваш github-репозиторий!
------
В начале terraform bin файл из предыдущего задания, скачал также отдельно:
![terrform-version](https://github.com/pythonyandex/Terraform_L1/blob/main/terraform_version.png)





### Задание 1

1. Перейдите в каталог [**src**](https://github.com/netology-code/ter-homeworks/tree/main/01/src). Скачайте все необходимые зависимости, использованные в проекте.

   _Все зависимости были скачаны._ 

3. Изучите файл **.gitignore**. В каком terraform-файле, согласно этому .gitignore, допустимо сохранить личную, секретную информацию?(логины,пароли,ключи,токены итд)
    
   personal.auto.tfvars - _Данный файл указан в .gitignore, его по традиции используют._

4. Выполните код проекта. Найдите  в state-файле секретное содержимое созданного ресурса **random_password**, пришлите в качестве ответа конкретный ключ и его значение.

   _Имеется ввиду параметр "result": "zOf7LvAMhr44aAin" в terraform.tfstate?_

6. Раскомментируйте блок кода, примерно расположенный на строчках 29–42 файла **main.tf**.
Выполните команду ```terraform validate```. Объясните, в чём заключаются намеренно допущенные ошибки. Исправьте их.

   _Ресурс docker_image должен иметь имя, например - "nginx":_
    resource "docker_image" "nginx" {
    name         = "nginx:latest"
    keep_locally = true
    }

   _Ресурс docker_container не может начинаться с цифры в имени._

8. Выполните код. В качестве ответа приложите: исправленный фрагмент кода и вывод команды ```docker ps```.

    _Файл main.tf_: [main.tf](https://github.com/pythonyandex/Terraform_L1/blob/main/main.tf)
_    Docker ps_:    ![docker ps](https://github.com/pythonyandex/Terraform_L1/blob/main/terraform_version.png)


10. Замените имя docker-контейнера в блоке кода на ```hello_world```. Не перепутайте имя контейнера и имя образа. Мы всё ещё продолжаем использовать name = "nginx:latest". Выполните команду ```terraform apply -auto-approve```.
   Объясните своими словами, в чём может быть опасность применения ключа  ```-auto-approve```. Догадайтесь или нагуглите зачем может пригодиться данный ключ? В качестве ответа дополнительно приложите вывод команды ```docker ps```.

     _Terraform автоматически применяет все изменения без запроса подтверждения от пользователя, нет возможности проверить план и можно уничтожить все одной неосторожной командой. Ключ, думаю, может пригодиться при автоматизации процессов._
     _Docker ps hello world_:    ![Docker ps hello world](https://github.com/pythonyandex/Terraform_L1/blob/main/docker_ps_hello_world.png)

12. Уничтожьте созданные ресурсы с помощью **terraform**. Убедитесь, что все ресурсы удалены. Приложите содержимое файла **terraform.tfstate**.

    _Файл terraform.tfstate_: [main.tf](https://github.com/pythonyandex/Terraform_L1/blob/main/terraform.tfstate)

14. Объясните, почему при этом не был удалён docker-образ **nginx:latest**. Ответ **ОБЯЗАТЕЛЬНО НАЙДИТЕ В ПРЕДОСТАВЛЕННОМ КОДЕ**, а затем **ОБЯЗАТЕЛЬНО ПОДКРЕПИТЕ** строчкой из документации [**terraform провайдера docker**](https://docs.comcloud.xyz/providers/kreuzwerker/docker/latest/docs).  (ищите в классификаторе resource docker_image )

    _Парамерт keep_locally = true в main.tf указывает, что образ должен остаться на локальной машине._
    keep_locally (Boolean) If true, then the Docker image won't be deleted on destroy operation. If this is false, it will delete the image from the docker local storage on destroy operation. [keep_locally](https://registry.terraform.io/providers/kreuzwerker/docker/latest/docs/resources/image)





