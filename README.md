# base

Jouer le playbook srv4.yml pour initier le compte ansible sur le server-4.scc-edu

```Shell
ansible-playbook -i inventory srv4.yml
```

Modifier le fichier d'inventaire pour retirer le commentaire sur le server-4.scc-edu


Importer les dépôts des travaux précédents et les mettre en place

### Nginx
```Shell
git clone https://github.com/normandie-demo/nginx.git
cd nginx
ansible-playbook -i ../inventory nginx.yml
```

### MariaDB

```Shell
cd ..
git clone https://github.com/normandie-demo/db.git
cd db
ansible-galaxy role install -r ./roles/requirements.yml -p ./roles
ansible-playbook -i ../inventory mariadb.yml
ansible-playbook -i ../inventory config.yml
ansible-playbook -i ../inventory init.yml
```
### Creation du Vault

Toujours dans le dossier db

```Shell
ansible-vault create mysql.yaml
```
insérer les informations en modifier les mots de passes à votre convenance

```Shell
old_pass: testPASS123
new_pass: testPASS456
```

Jouer le code

```Shell
ansible-playbook -i ../inventory -v replace.yml --ask-vault-pass
```

### Après mise en place Vault

Toujours dans le dossier db

```Shell
ansible-galaxy collection install community.mysql
ansible-playbook -i ../inventory -v db.yaml --ask-vault-pass
```