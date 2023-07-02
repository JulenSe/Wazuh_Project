**Prérequis**

Il faut avoir un serveur ansible configuré.

Pour qu'ansible puisse se déployer correctement, il faut que la clé ssh soit partagée avec les autres machines distantes.

En cas de besoin voici la documentation pour configurer et installer ansible:

https://documentation.wazuh.com/current/deployment-options/deploying-with-ansible/guide/install-ansible.html

Pour pouvoir déployer des playbook ansible sur windows il faut suivre cette documentation :
https://docs.ansible.com/ansible/latest/os_guide/index.html

Il faut aussi bien organiser son fichier hosts, et mettre les ips des terminaux dans les bonnes sections.
![image](https://github.com/JulenSe/Wazuh_Project/assets/54896656/c2db9e28-be96-4cb3-b191-b0feaa8988b0)

Les hostnames des machines distantes ne doivent pas avoir de caractère spécial, dans le hostname il ne doit y avoir que des chiffres, des lettres et aucun espace.

![image](https://github.com/JulenSe/Wazuh_Project/assets/54896656/d8ec3a8a-b28e-4d91-85f7-341322a97e3f)


Lorsqu’on lance le playbook wazuh-ossec.yml, il faut bien vérifier le chemin src, pour le vérifier, faites realpath ossec.conf

![image](https://github.com/JulenSe/Wazuh_Project/assets/54896656/f69998f6-9371-44a2-9e46-2642898a7d1c)

Veillez à bien mettre l’adresse ip de votre serveur wazuh dans la section soulignée.

La commande ppour lancer les playbook est la suivante : 
_ansible-playbook [le playbook] -b -K_

Lorsque tous les prérequis sont remplis, vous pouvez lancer les playbook dans cet ordre :
wazuh-indexer-and-dashboard.yml > wazuh-manager-oss.yml > wazuh-ossec.yml > wazuh-agent.yml

Configuration des alertes par e-mail

Ouvrez le fichier de configuration ossec.conf :
bash
sudo nano /var/ossec/etc/ossec.conf
Recherchez la section <global> et configurez les options d'e-mail comme suit :

![image](https://github.com/JulenSe/Wazuh_Project/assets/54896656/0e19b817-8bc8-4572-b82a-81ed969ed62f)

Assurez-vous de remplacer votre_email@example.com par votre adresse e-mail réelle et serveur_smtp.example.com par le serveur SMTP de votre fournisseur de messagerie.

Définissez le niveau d'alerte minimal qui déclenchera un e-mail en modifiant la valeur <email_alert_level> dans la section <alerts>. Par exemple :
xml

![image](https://github.com/JulenSe/Wazuh_Project/assets/54896656/46725744-aa86-4f83-aa08-c70dbe452810)

Cette valeur détermine le niveau minimal d'alerte pour lequel un e-mail sera envoyé.
Enregistrez les modifications et quittez l'éditeur de texte.

Redémarrage de Wazuh

Redémarrez le service Wazuh pour appliquer les modifications de configuration :

sudo systemctl restart wazuh-manager

Wazuh est maintenant configuré pour envoyer des alertes par e-mail.

