# Capture the Flag Warmup

### User Configuration
1. Add the following users
  * tony
  * bob
  * sarah
  * jenny
  * toto

1. Make sure that all users have to reset their password the next time they log in

1. Create the following groups
  * admin
  * devs
  * audit

1. Add the users to the following groups
  * admin
    * tony
    * sarah

  * developer
    * bob
    * tony
    * sarah
    * jenny

  * auditor
    * toto

1. Make sure that each user has the following directory structures in their home directories:
  * .ssh (user read/write/executable permissions)
    - generate an SSH key pair for each user in their directory
    - authorized_keys (user read/write permissions)
  * mysupersecret.txt (user read/write permissions)
  * mypublicsecret.txt (user read/write permissions, read for everyone)

1. Add 3 secret hidden files somewhere on the file system :
  * 1 that has the setid bit set (owned by root)
  * 1 that has the setuid and setgid bit set (owned by root)
  * 1 that has a flag in it with the following format: flag{sometexthere} (owned by any user)

1. Enable and harden SSH in the following ways:
  * Change default port
  * Disable root login
  * Don't allow any SSH password logins
