#  Règles de Détection Wazuh pour Active Directory

##  Description

Ce dépôt contient une série de règles personnalisées pour **Wazuh**, conçues pour détecter des comportements malveillants au sein d’un environnement **Active Directory (AD)**. L'objectif est d'améliorer la visibilité et la réactivité face aux attaques modernes, telles que le **Kerberoasting**, **Pass-the-Hash**, ou encore l'exécution d'outils comme **Mimikatz** ou **SharpHound**.

---

##  Contenu du document

Le document contient des cas d’usage et règles Wazuh pour les attaques suivantes :

###  Attaques d'identifiants
- DCSync (ID: 110001)
- Vidage de LSASS (ID: 100011)
- Exécution de Mimikatz (ID: 100000)
- Exploitation via rundll32.exe (ID: 100012)
- VaultCmd Credential Access (ID: 100013)
- Kerberoasting (ID: 110002)

###  Escalade de privilèges
- Ajout dans le groupe Administrateurs (ID: spécifique)
- Modifications du groupe **Group Policy Creator Owners** (ID: 111000)

###  Reconnaissance réseau
- Exécution de SharpHound (ID: 111151)
- Collectes avancées de SharpHound (ID: 111152)
- Requêtes LDAP suspectes (ID: 111154)

###  Exfiltration & persistance
- Création/modification de Web Shell (IDs: 100500, 100501)
- Fichiers ZIP créés par des exécutables (ID: 111156)
- Activités BloodHound via fichiers JSON (ID: 111153)

###  Ransomware
- Détection d’activités liées à **BlackBit** (IDs: 100106, 100107, 100108)

---

##  Utilisation

1. Copier les règles dans le fichier `rules/local_rules.xml` de Wazuh.
2. S'assurer que **Sysmon** est bien configuré pour générer les événements nécessaires.
3. Ajouter les définitions dans `ossec.conf` :
   ```xml
   <localfile>
     <location>Microsoft-Windows-Sysmon/Operational</location>
     <log_format>eventchannel</log_format>
   </localfile>
