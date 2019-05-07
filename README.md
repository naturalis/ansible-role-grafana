# grafana

Ansible role to setup grafana, includes datasources and dashboards managment. \
The latter ones are configured via API calls. API can be used remotely(e.g. localhost machine) or from currently managed machine.
To configure the origin of requests set `grafana__api_from_localhost` and `grafana__api_url` variables accordingly.

Compatible with Grafana 5.x., 6.x haven't been tested, 4.x became depricated.
Role works for both stand alone grafana and grafana in docker container

## Requirements

- Ansible >= 2.7

### Supported platforms

```yml
- EL
  - 7
- Ubuntu
  - xenial
  - bionic
```

## Default role variables

| Name | Description | Type | Default | Required |
| -----| ----------- | :--: | :------:| :------: |
| grafana__version | version of grafana, numeric string e.g. '5.4.2' or 'latest', capable with grafana 5.x | string | `5.4.2` | True |
| grafana__in_docker | If grafana should be installed as docker container | bool | `False` | True |
| grafana__api_from_localhost | use api calls from localhost or managed host | bool | `False` | True |
| grafana__api_url | API url of grafana for ansible modules | string | `http://localhost:{{ grafana__port }}` | True |
| grafana__no_log | flag for no_log of dasboards and datasources | bool | `True` | True |
| grafana__instance | instance name | string | `{{ ansible_host | default(inventory_hostname) }}` | True |
| grafana__logs_dir | path to logs | string | `/var/log/grafana` | True |
| grafana__data_dir | path to data dir | string | `/var/lib/grafana` | True |
| grafana__dir_dashboards | path to dashboards | string | `{{ grafana__data_dir }}/dashboards` | True |
| grafana__endpoint | grafana name/IP used in grafana_url | string | `None` | True |
| grafana__bind | FQDN adress for grafana http to listen | string | `0.0.0.0` | True |
| grafana__port | listening port | int | `3000` | True |
| grafana__url | external Grafana address - variable maps to 'root_url' in grafana server section | string | `http://{{ grafana__endpoint }}:{{ grafana__port }}` | True |
| grafana__domain | domain for grafana server | string | `{{ ansible_host | default('localhost') }}` | True |
| grafana__server | configuration of grafana server | dict | `look into defaults/yml` | True |
| grafana__security | None | dict | `look into default.yml` | True |
| grafana__database | database setup of grafana users and dashboards | dict | `{'type': 'sqlite3'}` | True |
| grafana__auth | Authentication mechanisms specification | dict | `{'basic': True}` | True |
| grafana__dashboards | dashboards to import with meta | string | `[]` | True |
| grafana__datasources | datasources to configure | list | `[]` | True |
| grafana__docker_config | Path to the grafana config - image volumes | string | `/etc/grafana/grafana.ini` | False |
| grafana__docker_data_dir | Path to the grafana data dir - image volumes | string | `None` | False |
| grafana__docker_log_dir | Path to the grafana log dir - image volumes | string | `None` | False |

**All default variables are described in [defaults/main.yml](defaults/main.yml) file.**

## Static role variables

This section describes static variables implemented in the role.

### Main variables

| Name | Description | Type | Default |
| -----| ----------- | :--: | :-----: |
| grafana__welcome_email_on_sign_up | sent email on sign up | bool | `False` |
| grafana__users | user management and registration | dict | `{'allow_sign_up': False, 'auto_assign_org_role': 'Viewer', 'default_theme': 'dark'}` |
| grafana__session | session management | dict | `{}` |
| grafana__analytics | reporting, bidning to Google analytics and check_for_updates | dict | `{}` |
| grafana__smtp | email notifications configuration | dict | `{}` |
| grafana__alerting | enable grafana alerting mechanism | bool | `True` |
| grafana__metrics | Configuration of Internal grafana metrics system | dict | `{}` |
| grafana__tracing | distributed tracing options | dict | `{}` |
| grafana__snapshots | configuration of snapshots | dict | `{}` |
| grafana__image_storage | configuration of external image storage | dict | `{}` |
| grafana__system_user | Grafana system username, used by docker configuration | string | `grafana` |
| grafana__system_group | Grafana system group, used by docker configuration | string | `grafana` |

**All static main variables are described in [vars/main.yml](vars/main.yml) file.**

## License

[Apache License 2.0](LICENSE)

## Support

ZeroDowntime <ansible@zerodowntime.pl>