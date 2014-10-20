# PHP-FPM

This role installs PHP-FPM (FastCGI Process Manager) which is an alternative PHP
FastCGI implementation with some additional features useful for sites of any size,
especially busier sites.

## Requirements

This role requires [Ansible](http://www.ansibleworks.com/) version 1.4 or higher
and the Debian/Ubuntu platform.

## Role Variables

The variables that can be passed to this role and a brief description about
them are as follows (additional variables are available in the source):

```yaml
phpfpm_pid: '/var/run/php5-fpm.pid'
phpfpm_error_log: 'STDERR'
phpfpm_log_level: 'notice'
phpfpm_emergency_restart_threshold: 10
phpfpm_emergency_restart_interval: '1m'
phpfpm_process_control_timeout: '10s'
phpfpm_user: 'nginx'
phpfpm_group: 'nginx'
phpfpm_use_socket: true

phpfpm_wwwpool_listen_socket: '/var/run/php5-fpm.sock'
phpfpm_wwwpool_listen_tcp: '127.0.0.1:9000'
phpfpm_wwwpool_listen_mode: '0666'
phpfpm_wwwpool_listen_allowed_clients: '127.0.0.1'
phpfpm_wwwpool_pm_max_children: 10
phpfpm_wwwpool_pm_start_servers: 4
phpfpm_wwwpool_pm_min_spare_servers: 2
phpfpm_wwwpool_pm_max_spare_servers: 6
phpfpm_wwwpool_pm_max_requests: 500
phpfpm_wwwpool_pm_status_path: ''
phpfpm_wwwpool_ping_path: ''
phpfpm_wwwpool_ping_response: 'pong'
phpfpm_wwwpool_slowlog: '/var/log/nginx/$pool.slow.log'
phpfpm_wwwpool_request_slowlog_timeout: '5s'
phpfpm_wwwpool_request_terminate_timeout: '120s'
phpfpm_wwwpool_rlimit_files: 131072
phpfpm_wwwpool_rlimit_core: 'unlimited'
phpfpm_wwwpool_chdir: '/'
phpfpm_wwwpool_catch_workers_output: 'yes'
```

### `php.ini` Configuration

```yaml
# Any valid configuration parameter from php.ini
phpini:
  short_open_tag: 'Off'
  zlib.output_compression: 'On'
  safe_mode: 'Off'
  realpath_cache_size: '128k'
  realpath_cache_ttl: 120
  zend.ze1_compatibility_mode: 'Off'
  expose_php: 'Off'
  max_execution_time: 120
  memory_limit: '128M'
```

### `apc.ini` Configuration

```yaml
# Any valid configuration parameter from apc.ini
phpapc:
  enabled: 1
  shm_segments: 1
  shm_size: '128M'
```

## Examples

1) Install PHP-FPM with defaults

    ```yaml
    ---
    # This playbook installs PHP-FPM

    - name: Apply PHP-FPM to all web nodes
      hosts: web_nodes
      roles:
        - php-fpm
    ```

2) Install PHP-FPM with custom variables

    ```yaml
    ---
    # This playbook installs PHP-FPM

    - name: Apply PHP-FPM to all web nodes
      hosts: web_nodes
      roles:
        - { role: php-fpm, phpini: {php_memory_limit: '256M'} }
    ```

## Dependencies

None.

## License

MIT.
