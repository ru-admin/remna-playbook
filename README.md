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
    pythhon3 -m venv .env
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
   `!!!ВНИМАНИЕ для запуска этого плейбука требуется чтобы имя пользователя на Github 
   совпадало с именем пользователя в all.yml`
   ```bash
     ansible-playbook prepare-playbook.yml -u root -k
   ```
   На первый вопрос вводим пароль от root
   Второй вопрос запрашивает пароль для пользователя
   
### Запустим установку remnawave:
  ```bash
     ansible-playbook playbook.yml -K
   ```
