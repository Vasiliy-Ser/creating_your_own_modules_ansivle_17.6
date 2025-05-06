# Домашнее задание к занятию 17.6 «Создание собственных модулей» - Падеев Василий

![answer1]()

## Подготовка к выполнению

1. Создайте пустой публичный репозиторий в своём любом проекте: `my_own_collection`.  
2. Скачайте репозиторий Ansible: `git clone https://github.com/ansible/ansible.git` по любому, удобному вам пути.  
3. Зайдите в директорию Ansible: `cd ansible`.  
4. Создайте виртуальное окружение: `python3 -m venv venv`.  
5. Активируйте виртуальное окружение: `. venv/bin/activate`. Дальнейшие действия производятся только в виртуальном окружении.  
6. Установите зависимости `pip install -r requirements.txt`.  
7. Запустите настройку окружения `. hacking/env-setup`.  
8. Если все шаги прошли успешно — выйдите из виртуального окружения `deactivate`.  
9. Ваше окружение настроено. Чтобы запустить его, нужно находиться в директории `ansible` и выполнить конструкцию `. venv/bin/activate && . hacking/env-setup`.  

## Основная часть

Ваша цель — написать собственный module, который вы можете использовать в своей role через playbook. Всё это должно быть собрано в виде collection и отправлено в ваш репозиторий.

**Шаг 1.** В виртуальном окружении создайте новый `my_own_module.py` файл.

**Шаг 2.** Наполните его содержимым:

**Шаг 3.** Заполните файл в соответствии с требованиями Ansible так, чтобы он выполнял основную задачу: module должен создавать текстовый файл на удалённом хосте по пути, определённом в параметре `path`, с содержимым, определённым в параметре `content`.

Создал [my_own_module.py](https://github.com/Vasiliy-Ser/creating_your_own_modules_ansivle_17.6/blob/fd26baeba22825631f7ca09d1f4eda2d5edf562e/ansible/lib/ansible/modules/my_own_module.py)

**Шаг 4.** Проверьте module на исполняемость локально.

![answer1](https://github.com/Vasiliy-Ser/creating_your_own_modules_ansivle_17.6/blob/fd26baeba22825631f7ca09d1f4eda2d5edf562e/png/7.png)

**Шаг 5.** Напишите single task playbook и используйте module в нём.

[playbook](https://github.com/Vasiliy-Ser/creating_your_own_modules_ansivle_17.6/blob/fd26baeba22825631f7ca09d1f4eda2d5edf562e/ansible/single_task_playbook.yml)

**Шаг 6.** Проверьте через playbook на идемпотентность.

![answer1](https://github.com/Vasiliy-Ser/creating_your_own_modules_ansivle_17.6/blob/fd26baeba22825631f7ca09d1f4eda2d5edf562e/png/7.png)

**Шаг 7.** Выйдите из виртуального окружения.

**Шаг 8.** Инициализируйте новую collection: `ansible-galaxy collection init my_own_namespace.yandex_cloud_elk`.

[collection](https://github.com/Vasiliy-Ser/creating_your_own_modules_ansivle_17.6/tree/fd26baeba22825631f7ca09d1f4eda2d5edf562e/my_own_namespace)

**Шаг 9.** В эту collection перенесите свой module в соответствующую директорию.

**Шаг 10.** Single task playbook преобразуйте в single task role и перенесите в collection. У role должны быть default всех параметров module.

![role](https://github.com/Vasiliy-Ser/creating_your_own_modules_ansivle_17.6/tree/fd26baeba22825631f7ca09d1f4eda2d5edf562e/my_own_namespace/yandex_cloud_elk/roles/single_task_role)

**Шаг 11.** Создайте playbook для использования этой role.

[playbook](https://github.com/Vasiliy-Ser/creating_your_own_modules_ansivle_17.6/blob/fd26baeba22825631f7ca09d1f4eda2d5edf562e/my_own_namespace/yandex_cloud_elk/playbook.yml)

**Шаг 12.** Заполните всю документацию по collection, выложите в свой репозиторий, поставьте тег `1.0.0` на этот коммит.

**Шаг 13.** Создайте .tar.gz этой collection: `ansible-galaxy collection build` в корневой директории collection.

[.tar.gzer1](https://github.com/Vasiliy-Ser/creating_your_own_modules_ansivle_17.6/blob/fd26baeba22825631f7ca09d1f4eda2d5edf562e/my_own_namespace/yandex_cloud_elk/my_own_namespace-yandex_cloud_elk-1.0.0.tar.gz)

**Шаг 14.** Создайте ещё одну директорию любого наименования, перенесите туда single task playbook и архив c collection.

**Шаг 15.** Установите collection из локального архива: `ansible-galaxy collection install <archivename>.tar.gz`.

![answer1](https://github.com/Vasiliy-Ser/creating_your_own_modules_ansivle_17.6/blob/fd26baeba22825631f7ca09d1f4eda2d5edf562e/png/12.png)

**Шаг 16.** Запустите playbook, убедитесь, что он работает.

![answer1](https://github.com/Vasiliy-Ser/creating_your_own_modules_ansivle_17.6/blob/fd26baeba22825631f7ca09d1f4eda2d5edf562e/png/16.png)

**Шаг 17.** В ответ необходимо прислать ссылки на collection и tar.gz архив, а также скриншоты выполнения пунктов 4, 6, 15 и 16.

## Необязательная часть

1. Реализуйте свой модуль для создания хостов в Yandex Cloud.
2. Модуль может и должен иметь зависимость от `yc`, основной функционал: создание ВМ с нужным сайзингом на основе нужной ОС. Дополнительные модули по созданию кластеров ClickHouse, MySQL и прочего реализовывать не надо, достаточно простейшего создания ВМ.
3. Модуль может формировать динамическое inventory, но эта часть не является обязательной, достаточно, чтобы он делал хосты с указанной спецификацией в YAML.
4. Протестируйте модуль на идемпотентность, исполнимость. При успехе добавьте этот модуль в свою коллекцию.
5. Измените playbook так, чтобы он умел создавать инфраструктуру под inventory, а после устанавливал весь ваш стек Observability на нужные хосты и настраивал его.
6. В итоге ваша коллекция обязательно должна содержать: clickhouse-role (если есть своя), lighthouse-role, vector-role, два модуля: my_own_module и модуль управления Yandex Cloud хостами и playbook, который демонстрирует создание Observability стека.


