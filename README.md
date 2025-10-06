# Ansible Role: smb client

[![CI](https://github.com/Tinyblargon/ansible-role-smb-client/actions/workflows/ci.yml/badge.svg)](https://github.com/Tinyblargon/ansible-role-smb-client)

Install dependencies for smb and add credentials.

## Requirements

N/A

## Role Variables

### Defaults

| **Variable Name**      | **Type**| **Default Value**     | **Description**|
| :----------------------| :------:| :--------------------:| :--------------|
| smb_client_credentials:| list map| []                    | List of credentials, see: [Smb_client_credentials](#smb_client_credentials).|
| smb_client_folder:     | string  | "/opt/.smbcredentials"| The folder in which the credential files will bes stored.|
| smb_client_remove:     | bool    | false                 | When `true` all unspecified files in `smb_client_folder:` will be removed.|
| smb_client_state:      | string  | "present"             | When `"present"` smb client will be installed, and credential file created. When `"absent"` smb client and credential files will be removed.|

### Smb_client_credentials

| **Variable Name**| **Required**| **Type**| **Default Value**| **Description**|
| :----------------| :----------:| :------:| :---------------:| :--------------|
| name:            | yes         | string  | ""               | This is the name of the smb credentails file.|
| username:        | no          | string  | ""               | The username for the SMB connection.|
| password         | no          | string  | ""               | The password for the SMB connection.|
| domain:          | no          | string  | ""               | The domain for the SMB connection.|
| state:           | no          | string  | "present"        | When `"present"` the credential file will be created, when `"absent"` the credential file will be removed.|

## Dependencies

N/A

## Example Playbook

```yml
- hosts: all
  roles:
    - role: tinyblargon.smb_client
      vars:
        smb_client_credentials:
          - name: "creds-nas"
            username: "{{ lookup('file', '.secrets/smb-username') }}"
            password: "{{ lookup('file', '.secrets/smb-password') }}"
            domain: "example.com"
          - name: "creds-old"
            state: "absent"
        smb_client_remove: true
        smb_client_state: "present"
```

## License

MIT
