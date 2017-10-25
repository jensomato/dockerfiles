# Self-Service-Password
[Self Service Password](https://ltb-project.org/documentation/self-service-password) is a PHP application that allows users to change their password in an LDAP directory.

The application can be used on standard LDAPv3 directories (OpenLDAP, OpenDS, ApacheDS, Sun Oracle DSEE, Novell, etc.) and also on Active Directory.

The Application is developed by [LDAP Tool Box Project](https://ltb-project.org)

## Usage
The most common configuration parameters can be set by the following environment variables. Please read the [documentation](https://ltb-project.org/documentation/self-service-password/1.2/start) for the valid configuration values or have a look at the [default configuration file](https://github.com/ltb-project/self-service-password/blob/master/conf/config.inc.php).  

| ENV Variable | Config Variable | Type | Default Value |
| -------- | -------- | -------- | -------- |
| LDAP_URL     | $ldap_url     | Text     |ldap://localhost|
| LDAP_STARTTLS     | $ldap_starttls     | Boolean     | `false` |
| LDAP_BINDDN     | $ldap_binddn     | Text     |cn=manager,dc=example,dc=com|
| LDAP_BINDPW     | $ldap_bindpw     | Text     |secret|
| LDAP_BASE     | $ldap_base     | Text     |dc=example,dc=com|
| LDAP_LOGIN_ATTR     | $ldap_login_attribute     | Text     |uid|
| LDAP_FULLNAME_ATTR     | $ldap_fullname_attribute     | Text     |cn|
| LDAP_FILTER     | $ldap_filter     | Text     |(&(objectClass=person)($ldap_login_attribute={login}))|
| HASH     | $hash     | Text     |clear|
| USE_QUESTIONS     | $use_questions     | Boolean     |true|
| USE_TOKENS     | $use_tokens     | Boolean     |true|
| MAIL_ATTRIBUTE     | $mail_attribute     | Text     |mail|
| MAIL_ADDRESS_USE_LDAP     | $mail_address_use_ldap     | Boolean     |false|
| MAIL_FROM     | $mail_from     | Text     |admin@example.com|
| MAIL_FROM_NAME     | $mail_from_name     | Text     |Self Service Password|
| MAIL_SIGNATURE     | $mail_signature     | Text     ||
| MAIL_NOTIFY_ON_CHANGE     | $notify_on_change     | Boolean     |false|
| MAIL_PROTOCOL     | $mail_protocol     | Text     |smtp|
| MAIL_SMTP_HOST     | $mail_smtp_host     | Text     |localhost|
| MAIL_SMTP_AUTH     | $mail_smtp_auth     | Boolean     |false|
| MAIL_SMTP_USER     | $mail_smtp_user     | Text     ||
| MAIL_SMTP_PASS     | $mail_smtp_pass     | Text     ||
| MAIL_SMTP_PORT     | $mail_smtp_port     | Number     |25|
| MAIL_SMTP_SECURE     | $mail_smtp_secure     | Text     |tls|
| USE_SMS     | $use_sms     | Boolean     |true|

If you have more specific configuration needs you can also provide your own configuration file to the container. The config file is named `config.inc.php` and has to be mounted to `/usr/share/self-service-password/conf/config.inc.php` in the container like this

```
docker run -v /path/to/your/config.inc.php:/usr/share/self-service-password/conf/config.inc.php jensomato/self-service-password
```


