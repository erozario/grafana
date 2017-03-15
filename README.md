Grafana
=========

Installs and setup Grafana metrics dashboard and Nginx proxy_pass


Installation
------------

erozario.grafana is an Ansible role distributed globally using Ansible Galaxy. In order to install erozario/grafana role you can use the following command.

    $ ansible-galaxy install erozario.grafana

Role Variables
--------------

    - vars:

      grafana_enabled: true

      grafana_version: latest

      grafana_app_mode: production

      # Paths
      grafana_data: /var/lib/grafana
      grafana_logs: /var/log/grafana
      grafana_plugins: "{{ grafana_data }}/plugins"
      grafana_plugins_install: []

      # Server
      grafana_protocol: http
      grafana_http_addr: 0.0.0.0
      grafana_http_port: 3000
      grafana_domain: localhost
      grafana_enforce_domain: false
      grafana_root_url: "%(protocol)s://%(domain)s:%(http_port)s/"
      grafana_router_logging: false
      grafana_static_root_path: public
      grafana_enable_gzip: false
      grafana_cert_file:
      grafana_cert_key:

      # Database
      grafana_type: sqlite3
      grafana_host: 127.0.0.1:3306
      grafana_name: grafana
      grafana_user: root
      grafana_password:
      grafana_ssl_mode: disable
      grafana_path: grafana.db

      # Session
      grafana_provider: file
      grafana_provider_config: sessions
      grafana_cookie_name: grafana_sess
      grafana_cookie_secure: false
      grafana_session_life_time: 86400

      # Analytics
      grafana_reporting_enabled: false
      grafana_check_for_updates: false
      grafana_google_analytics_ua_id:

      # Security
      grafana_admin_user: admin
      grafana_admin_password: admin
      grafana_secret_key: admin
      grafana_login_remember_days: 7
      grafana_cookie_username: grafana_user
      grafana_cookie_remember_name: grafana_remember
      grafana_disable_gravatar: false
      grafana_data_source_proxy_whitelist:

      # Snapshots
      grafana_external_enabled: false
      grafana_external_snapshot_url:
      grafana_external_snapshot_name:

      # Users
      grafana_allow_sign_up: true
      grafana_allow_org_create: true
      grafana_auto_assign_org: true
      grafana_auto_assign_org_role: Viewer
      grafana_login_hint: email or username

      # Anonymous Auth
      grafana_anonymous_enabled: false
      grafana_anonymous_org_name: Main Org.
      grafana_anonymous_org_role: Viewer

      # Github Auth
      grafana_github_enabled: false
      grafana_github_client_id: some_id
      grafana_github_client_secret: some_secret
      grafana_github_scopes: user:email
      grafana_github_auth_url: https://github.com/login/oauth/authorize
      grafana_github_token_url: https://github.com/login/oauth/access_token
      grafana_github_api_url: https://api.github.com/user
      grafana_github_team_ids:
      grafana_github_allowed_organizations:
      grafana_github_auth_allow_sign_up: true

      # Google Auth
      grafana_google_enabled: false
      grafana_google_client_id: some_id
      grafana_google_client_secret: some_secret
      grafana_google_scopes: https://www.googleapis.com/auth/userinfo.profile https://www.googleapis.com/auth/userinfo.email
      grafana_google_auth_url: https://accounts.google.com/o/oauth2/auth
      grafana_google_token_url: https://accounts.google.com/o/oauth2/token
      grafana_google_api_url: https://www.googleapis.com/oauth2/v1/userinfo
      grafana_google_allowed_domains: mycompany.com othercompany.com
      grafana_google_auth_allow_sign_up: true

      # Basic Auth
      grafana_auth_basic_enabled: true

      # Auth Proxy
      grafana_auth_proxy_enabled: false
      grafana_auth_proxy_header_name: X-WEBAUTH-USER
      grafana_auth_proxy_header_property: username
      grafana_auth_proxy_auto_sign_up: true

      # Auth LDAP
      grafana_auth_ldap_enabled: false
      grafana_auth_ldap_config_file: /etc/grafana/ldap.toml

      # SMTP / Emailing
      grafana_smtp_enabled: false
      grafana_smtp_host: localhost:25
      grafana_smtp_user:
      grafana_smtp_password:
      grafana_smtp_cert_file:
      grafana_smtp_key_file:
      grafana_smtp_skip_verify: false
      grafana_smtp_from_address: admin@grafana.localhost
      grafana_emails_welcome_email_on_sign_up: false

      # Logging
      grafana_log_mode: console, file
      grafana_log_buffer_len: 10000
      grafana_log_level: Info

      # AMPQ Event Publisher
      grafana_ampq_enabled: false
      grafana_ampq_rabbitmq_url: amqp://localhost/
      grafana_ampq_exchange: grafana_events

      # Dashboard JSON files
      grafana_dashboard_json_enabled: false
      grafana_dashboard_json_path: /var/lib/grafana/dashboards

      # Setup nginx configuration
      grafana_nginx: false
      grafana_nginx_servername: "{{inventory_hostname}}"
      grafana_nginx_ssl: false
      grafana_nginx_ssl_crt: ""
      grafana_nginx_ssl_key: ""
      grafana_nginx_ssl_redirect: "{{grafana_nginx_ssl}}"
      grafana_nginx_port: 80


Dependencies
------------

    $ ansible-galaxy install geerlingguy.nginx

Example Playbook
----------------

    - hosts: all
      become: yes
       roles:
        - erozario.grafana
        - geerlingguy.nginx
      vars:
        grafana_admin_user: admin
        grafana_admin_password: grafana
        grafana_plugins_install: [alexanderzobnin-zabbix-app, grafana-worldmap-panel]

License
-------

MIT

Author Information
------------------
https://www.linkedin.com/in/eduardo-rozario/
