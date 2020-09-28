Domain Join
===========

Ansible роль для присоединения хостов к домену Active Directory и для управления локальными администраторами.

Требования
----------

- Поддерживаемая версия Ansible: 2.7 и выше.
- `pywinrm` для подключения [Ansible через WinRM](https://docs.ansible.com/ansible/latest/user_guide/windows_winrm.html) (для Windows).
- Список поддерживаемых платформ описан в файле метаданных роли.

Используемые переменные
-----------------------

- `domain_join__dns_domain_name` DNS имя домена Active Directory.
- `domain_join__domain_controllers` Список контроллеров домена.
- `domain_join__username` Логин пользователя, из под которого осуществляется присоединение к домену.

  **Внимание** Если пользователь не является администратором, то нужно убедиться, что ему делегированы права на создание и изменение объектов компьютера, а также на чтение/запись атрибутов `operatingSystem` и `operatingSystemVersion`.

- `domain_join__password` Пароль пользователя, из под которого осуществляется присоединение к домену.
- `domain_join__ou_path` Организационная единица, в которую будет помещён объект компьютера после присоединения к домену.
- `domain_join__admin_groups` Список доменных групп, пользователи которых будут являться локальными администраторами.

Зависимости
-----------

Отсутствуют.

Пример использования
--------------------

```yaml
---

- name: Join Into Domain
  hosts: all

  roles:
    - role: domain-join
      domain_join__dns_domain_name: domain.local
      domain_join__domain_controllers:
        - dc-01.domain.local
        - dc-02.domain.local
      domain_join__username: Administrator
      domain_join__password: P@ssw0rd!
      domain_join__ou_path: OU=Servers,DC=domain,DC=local
      domain_join__admin_groups:
        - sysadmins
```

Лицензия
--------

MIT

Информация об авторе
--------------------

Мелехин Антон, ООО "ЖИЛИЩНАЯ ЭКОСИСТЕМА ВТБ".
