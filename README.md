# spiivt_3

1. Создать пользователя

useradd webmaster

и задать ему пароль

passwd webmaster

2. Создать SELinux пользователя webadm_u

semanage user -a -R "staff_r system_r webadm_r" -L s0 -r s0 webadm_u

после логина получаем

id -Z

unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023

3. сопоставление пользователя linux и SELinux

semanage login -a -r s0 -s webadm_u webmaster

4. скопировать шаблон staff_u в webadm_u

cp /etc/selinux/targeted/contexts/users/staff_u /etc/selinux/targeted/contexts/users/webadm_u


после логина получаем

id -Z

webadm_u:staff_r:staff_t:s0

то что нужно

5. Добавить правило для sudoers

echo 'webmaster ALL=(ALL) TYPE=webadm_t ROLE=webadm_r ALL' > /etc/sudoers.d/webmaster

после этого проверяем, логинимся

sudo systemctl restart httpd

команда выполняется

sudo date 022118442016

/bin/date: cannot set date: Operation not permitted


