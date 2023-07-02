Prérequis

Il faut avoir un serveur ansible configuré.

Pour qu'ansible puisse se déployer correctement, il faut que la clé ssh soit partager avec les autres machines distantes.

En cas de besoin voici la documentation pour configurer et installer ansible:

https://documentation.wazuh.com/current/deployment-options/deploying-with-ansible/guide/install-ansible.html

Et pour pouvoir déployer des playbook ansible sur windows il faut suivre cette documentation :
https://docs.ansible.com/ansible/latest/os_guide/index.html

Il faut aussi bien organiser son fichier hosts, et mettre les ips des terminaux dans les bonnes sections.
![image](https://github.com/JulenSe/Wazuh_Project/assets/54896656/adade9f8-f815-4300-99d9-1f998552843e)

Les hostnames des machines distantes ne doivent pas avoir de caractère spécial, dans le hostname il ne doit y avoir que des chiffres, des lettres et aucun espace.

![image](https://github.com/JulenSe/Wazuh_Project/assets/54896656/382452e9-8389-49e5-abf5-1c5e672b2180)

Lorsqu’on lance le playbook wazuh-ossec.yml, il faut bien vérifier le chemin src, pour le vérifier faite realpath ossec.conf

![image](https://github.com/JulenSe/Wazuh_Project/assets/54896656/e5b4fcf5-d4f0-4c49-895c-2af3f9eff370)

Veillez à bien mettre l’adresse ip de votre serveur wazuh dans la section sousligné.

Lorsque tous les prérequis sont remplis, vous pouvez lancer les playbook dans cet ordre :
wazuh-indexer-and-dashboard.yml > wazuh-manager-oss.yml > wazuh-ossec.yml > wazuh-agent.yml

