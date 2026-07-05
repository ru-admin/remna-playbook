# Ансибл плейбук для развертывания remnawave

  Данный плейбук предназначен для развертывания и поддержки проекта [remna.st](https://remna.st).

## Краткая инструкция по использованию (на Linux)

### Склонируем и перейдем в директорию с плейбуком
  ```bash
    git clone https://github.com/iphizic/remna-playbook.git
    cd remna-playbook
  ```

### Сначала подготовим  Python .env:
  ```bash
    python3 -m venv .env
  ```

### Активируем .env:
  ```bash
    source .env/bin/activate
  ```
### Установим Ansible и зависимости:
  ```bash
    pip install -r requirements.txt
    ansible-galaxy install -r requirements.yml
  ```
### Сформируем и отредактируем инвентарь и прочие переменные 
  Инвентарь можно сформировать согласно inventory.yml.example в директории inventory
  В директории group_vars необходимо сформировать all.yml согласно all.yml.example

### `Опционально` Создадим пользователя отличного от root для хоста
   Два варианта плейбука для создания пользователя:

   **Вариант 1: Ключи с GitHub**
   ```bash
     ansible-playbook prepare_playbook.yml -u root -b
   ```
   Ключи загружаются автоматически с `https://github.com/<user>.keys`

   **Вариант 2: Локальные ключи**
   ```bash
     ansible-playbook prepare_playbook_localkeys.yml -u root -b
   ```
   Ключи берутся из `group_vars/all.yml`. Требуется настройка переменной `default_user_authorized_keys`:
   ```yaml
   default_user_authorized_keys:
     - "ssh-ed25519 AAAA... user1@host"
     - "ssh-ed25519 AAAA... user2@host"
   ```

   На первый вопрос вводим пароль от root
   Второй вопрос запрашивает пароль для пользователя

   **Важно:** файл `group_vars/all.yml` добавлен в `.gitignore`, поэтому ваши ключи не попадут в репозиторий.
   
### Запустим установку remnawave:
   ```bash
     ansible-playbook playbook.yml
   ```
   Если переменная `user_password` задана в `group_vars/all.yml`, пароль подставится автоматически.
   Если переменная не задана, запускайте с флагом `-K` для ручного ввода:
   ```bash
     ansible-playbook playbook.yml -K
   ```
