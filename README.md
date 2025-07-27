# Ansible Server Provisioning

## Подготовка целевого сервера

1. Установить и включить SSH-сервер:
   ```bash
   apt update && apt install -y openssh-server
   systemctl enable ssh
   ```

2. Убедиться, что в файле `/etc/ssh/sshd_config` указано:
   ```
   PermitRootLogin prohibit-password
   ```

3. Добавить публичный SSH-ключ в `/root/.ssh/authorized_keys` на целевой машине.

## Настройка перед запуском

1. В файле `inventory.ini` заменить IP `192.168.0.30` на IP целевой машины.

2. Создать файл `.vault_pass.txt` с правами доступа 600 в корне репозитория и вставить в него:
   ```
   123
   ```

3. Установить переменные окружения:
   ```bash
   export ANSIBLE_PRIVATE_KEY_FILE=/путь/до/закрытого_ключа
   export ANSIBLE_CONFIG=ansible.cfg
   ```

   ansible.cfg лежит в корне репозитория

## Запуск плейбука

```bash
ansible-playbook playbook.yml
```
