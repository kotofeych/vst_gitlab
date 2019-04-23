vst_gitlab
===========
This Ansible role installs and configures GitLab.

Dependency:
-----------
* `geerlingguy.gitlab`

## The main variables that must be specified:
```yaml
vst_gitlab_name_host: 'example.com'
letsencrypt_contact_email: 'example@example.com'
```
* if `letsencrypt_enable: false` you dont need specify `letsencrypt_contact_email`

## Additional variables that can be edited:

#### The template config file to GitLab
```yaml
vst_gitlab_time_zone: 'Asia/Vladivostok'
```
#### PROJECTS FEATURES
```yaml
gitlab_rails_gitlab_default_projects_features_issues: 'true'
gitlab_rails_gitlab_default_projects_features_merge_requests: 'true' 
gitlab_rails_gitlab_default_projects_features_wiki: 'true'
gitlab_rails_gitlab_default_projects_features_snippets: 'true'
gitlab_rails_gitlab_default_projects_features_builds: 'true'
gitlab_rails_gitlab_default_projects_features_container_registry: 'true'
gitlab_rails_gitlab_issue_closing_pattern: '((?:[Cc]los(?:e[sd]?|ing)|[Ff]ix(?:e[sd]|ing)?|[Rr]esolv(?:e[sd]?|ing)|[Ii]mplement(?:s|ed|ing)?)(:?) +(?:(?:issues? +)?%{issue_ref}(?:(?:, *| +and +)?)|([A-Z][A-Z0-9_]+-\\d+))+)'
```
#### ARTIFACTS
```yaml
gitlab_rails_artifacts_enabled : 'true'
gitlab_rails_artifacts_path: '/var/opt/gitlab/gitlab-rails/shared/artifacts'
```
#### LFS
```yaml
gitlab_rails_lfs_enabled: 'true'
```
#### NGINX
```yaml
nginx_enable: 'true'
nginx_dir: '/var/opt/gitlab/nginx'
nginx_log_directory: '/var/log/gitlab/nginx'
nginx_gzip: on
nginx_worker_processes: 4
nginx_cache_max_size: '5000m'
```
#### LETSECRYPT
```yaml
letsencrypt_enable: 'true'
letsencrypt_contact_email: 'example@gmail.com'
letsencrypt_auto_renew: 'true'
```

#### Backup upload
* If you use cloud for storage
```yaml
gitlab_rails_backup_upload_connection_provider: 'example'
gitlab_rails_backup_upload_connection_region: 'example'
gitlab_rails_backup_upload_connection_aws_access_key_id: 'example'
gitlab_rails_backup_upload_connection_aws_secret_access_key: 'example'
gitlab_rails_backup_upload_connection_endpoint: 'example'
```
```yaml
gitlab_rails_backup_archive_permissions: 0644
gitlab_rails_backup_upload_remote_directory: 'gitlab-backups'
gitlab_rails_backup_storage_class: 'STANDARD'
```

#### Grafana
```yaml
grafana_enable: 'true'
grafana_admin_password: '123456'
```

#### Mattermost config
```yaml
mattermost_enable: 'true'
gitlab_subdomain_chat: 'chat'
mattermost_team_site_name: 'Chat GitLab'
mattermost_env_MM_SERVICESETTINGS_MAXIMUMLOGINATTEMPTS: 15
mattermost_env_MM_TEAMSETTINGS_TEAMMATENAMEDISPLAY: 'full_name'
mattermost_env_MM_SQLSETTINGS_MAXIDLECONNS: 10
mattermost_env_MM_LOGSETTINGS_FILELEVEL: 'DEBUG'
mattermost_env_MM_EMAILSETTINGS_BATCHINGINTERVAL: 30
mattermost_env_MM_SUPPORTSETTINGS_SUPPORTEMAIL: 'email@example.com'
mattermost_env_MM_FILESETTINGS_ENABLEFILEATTACHMENTS: 'true'
mattermost_env_MM_RATELIMITSETTINGS_MEMORYSTORESIZE: 10000
mattermost_env_MM_PRIVACYSETTINGS_SHOWEMAILADDRESS: 'true'
mattermost_env_MM_LOCALIZATIONSETTINGS_AVAILABLELOCALES: 'en,ru'
mattermost_env_MM_WEBRTCSETTINGS_ENABLE: 'false'
mattermost_env_MM_LOCALIZATIONSETTINGS_DEFAULTSERVERLOCALE: en
mattermost_env_MM_EMAILSETTINGS_ENABLESIGNUPWITHEMAIL: 'false'
mattermost_env_MM_EMAILSETTINGS_ENABLESIGNINWITHEMAIL: 'true'
mattermost_env_MM_EMAILSETTINGS_ENABLESIGNINWITHUSERNAME: 'true'
mattermost_env_MM_EMAILSETTINGS_SENDEMAILNOTIFICATIONS: 'true'
mattermost_env_MM_EMAILSETTINGS_REQUIREEMAILVERIFICATION: 'true'
mattermost_env_MM_EMAILSETTINGS_FEEDBACKNAME: 'Chat Gitlab'
mattermost_env_MM_EMAILSETTINGS_CONNECTIONSECURITY: 'TLS'
mattermost_env_MM_EMAILSETTINGS_SENDPUSHNOTIFICATIONS: 'true'
mattermost_env_MM_PLUGINSETTINGS_ENABLEUPLOADS: 'true'
mattermost_env_MM_SERVICESETTINGS_ENABLEINCOMINGWEBHOOKS: 'true'
mattermost_env_MM_SERVICESETTINGS_ENABLEPOSTICONOVERRIDE: 'true'
mattermost_env_MM_SERVICESETTINGS_ENABLEOUTGOINGWEBHOOKS: 'true'
mattermost_env_MM_SERVICESETTINGS_ENABLECOMMANDS: 'true'
mattermost_env_MM_SERVICESETTINGS_ENABLELINKPREVIEWS: 'true'
mattermost_env_MM_SERVICESETTINGS_ENABLEUSERTYPINGMESSAGES: 'true'
mattermost_env_MM_SERVICESETTINGS_ENABLEPOSTSEARCH : 'true'
mattermost_env_MM_SERVICESETTINGS_ENABLEUSERSTATUSES: 'true'
mattermost_env_MM_TEAMSETTINGS_ENABLETEAMCREATION: 'false'
mattermost_env_MM_TEAMSETTINGS_ENABLEUSERCREATION: 'true'
```

#### Registry 
```yaml
registry_enable: 'true'
gitlab_subdomain_registry: 'registry'
registry_storagedriver_health_enabled: 'true'
```

* If you use cloud for storage
```yaml
registry_storage_swift_username: 'example'
registry_storage_swift_password: 'example'
registry_storage_swift_authurl: 'example'
registry_storage_swift_domainid: 'example'
registry_storage_swift_container: 'example'
```

#### Omnibus GitLab Logs
```yaml
logrotate_enable: 'true'
logging_logrotate_frequency: 'daily'
logging_logrotate_rotate: 30
logging_logrotate_compress: 'compress'
```

#### Pages
```yaml
gitlab_pages_enable: 'true'
gitlab_subdomain_pages: 'pages'
gitlab_pages_access_control: 'true'
gitlab_pages_log_verbose: 'true'
```

Example playbook:
=================
```yaml
- hosts: all
  become: yes
  vars:
      vst_gitlab_name_host: 'example.com'
      letsencrypt_contact_email: 'example@example.com'
  roles:
    - role: kotofeych.vst_gitlab
```

License
-------
BSD

Author Information
------------------
[Konstantin Shumkin](https://github.com/kotofeych)

