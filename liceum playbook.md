
```yml
- hosts: all
  become: true
  tasks:
    - name: Корневой сертификат
      copy:
        src: russian_trusted_root_ca_pem.crt
        dest: /usr/share/pki/ca-trust-source/anchors
        mode: 0644

    - name: Выпускающий сертификат
      copy:
        src: russian_trusted_sub_ca_pem.crt
        dest: /usr/share/pki/ca-trust-source/anchors
        mode: 0644

    - name: Обновление сертификата
      command: sudo update-ca-trust

	- name: Список пакетов
	      apt:
	        pkg:
	        - 1
	        - 2
	        - 3
	        - ...

```

## Inventory

```yml
[servers]
192.168.0.100-192.168.0.226 ansible_port=22 ansible_user=user ansible_password=password ansible_connection=ssh

```

# Установка

Ubuntu/Debian:
```bash
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible
```

Проверка версии ansible:
```bash
ansible --version
```

# Настройка конфига
```bash
nano ansible.config
```

Пример конфига:
```bash
[defaults]

#файл с базовыми настройками наших клиентов
inventory = /ПУТЬ_К_ФАЙЛУ

#отключаем проверку рукопожатия
host_key_checking = False
```

Проверка работоспособности:
```bash
ansible -m ping
```

Запуск плейбука:
```bash
ansible-playbook install.yml
```