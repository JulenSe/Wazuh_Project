Prérequis

Il faut avoir un serveur ansible configuré.

Pour qu'ansible puisse se déployer correctement, il faut que la clé ssh soit partagée avec les autres machines distantes.

En cas de besoin voici la documentation pour configurer et installer ansible:

https://documentation.wazuh.com/current/deployment-options/deploying-with-ansible/guide/install-ansible.html

Pour pouvoir déployer des playbook ansible sur windows il faut suivre cette documentation :
https://docs.ansible.com/ansible/latest/os_guide/index.html

Il faut aussi bien organiser son fichier hosts, et mettre les ips des terminaux dans les bonnes sections.
![image](https://github.com/JulenSe/Wazuh_Project/assets/54896656/adade9f8-f815-4300-99d9-1f998552843e)

Les hostnames des machines distantes ne doivent pas avoir de caractère spécial, dans le hostname il ne doit y avoir que des chiffres, des lettres et aucun espace.

![image](https://github.com/JulenSe/Wazuh_Project/assets/54896656/382452e9-8389-49e5-abf5-1c5e672b2180)

Lorsqu’on lance le playbook wazuh-ossec.yml, il faut bien vérifier le chemin src, pour le vérifier, faites realpath ossec.conf

![image](https://github.com/JulenSe/Wazuh_Project/assets/54896656/e5b4fcf5-d4f0-4c49-895c-2af3f9eff370)

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
<ossec_config><global><email_notification>yes</email_notification><email_to>votre_email@example.com</email_to><smtp_server>serveur_smtp.example.com</smtp_server><email_from>wazuh@example.com</email_from></global>
    ...
</ossec_config>

Assurez-vous de remplacer votre_email@example.com par votre adresse e-mail réelle et serveur_smtp.example.com par le serveur SMTP de votre fournisseur de messagerie.

Définissez le niveau d'alerte minimal qui déclenchera un e-mail en modifiant la valeur <email_alert_level> dans la section <alerts>. Par exemple :
xml

<ossec_config><alerts><email_alert_level>10</email_alert_level></alerts>
  ...
</ossec_config>
Cette valeur détermine le niveau minimal d'alerte pour lequel un e-mail sera envoyé.
Enregistrez les modifications et quittez l'éditeur de texte.

Redémarrage de Wazuh

Redémarrez le service Wazuh pour appliquer les modifications de configuration :

sudo systemctl restart wazuh-manager

Wazuh est maintenant configuré pour envoyer des alertes par e-mail.

