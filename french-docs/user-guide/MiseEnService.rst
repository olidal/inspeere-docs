.. _mise_en_service:

2. Mise en service
------------------

Selon la prestation d'installation retenue en collaboration avec votre 
revendeur, votre solution Inspeere peut être livrée soit pré-installée et 
pré-activée, soit prête à être activée sur site. 

Dans les deux cas votre revendeur assurera la réalisation 
des étapes suivantes de l'installation, dans vos locaux:

* :ref:`mise_en_place`
* :ref:`ip_statique`
* :ref:`config_dnat`
* :ref:`filtrage_sortant`
* :ref:`config_backup`
* :ref:`compte_admin`

En tant que client, vous n'avez pas à vous soucier de ces étapes d'installation. 
La mise en oeuvre de ces prescriptions est assurée par un **technicien spécialiste 
formé par Inspeere**.

Dans les cas les plus simples, la mise en service se fait en moins d'une heure.
Son déroulé est le suivant:

1. **Mise en place physique** : déballage, mise en place, connexion au réseau, ...
2. **Configuration IP statique** : la DATIS a besoin d'une adresse permanente, qui ne change pas, car elle fonctionne comme un serveur et doit pouvoir être facilement localisée par les postes et utilisateurs sur le réseau interne
3. **Démarrage équipement** : bouton on/off
4. **Défiltrage sortant** : sur certains sites, le prestatire informatique en charge de la politique de sécurité peut avoir mis en place certains filtrages au niveau du pare-feux qui pourraient empêcher la DATIS de joindre certains services sur Internet. Ces réglages doivent éventuellement íetre corrigés pour permettre à la DATIS de fonctionner normalement
5. **Configuration DNAT** : le principe de la sauvegarde mutuelle implique que d'autres DATIS doivent pouvoir envoyer des donner à votre DATIS (de façon TRÈS sûre!), ce qui requiert aussi un réglage au niveau de votre pare-feux 
6. **Déploiement des clients de sauvegarde** (sur les postes de travail) : un petit programme doit être installé sur chacun des postes de travail que vous souhaitez sauvegarder.

Puis, 30mins au moins après l'étape 3 (le temps que la Datis s'auto-configure):

7. Création d'un compte Administrateur : chaque DATIS embarque une interface de configuration, DatisAdmin, qui peut être jointe à partir de votre réseau local, et qui permet la créeation de comptes utilisateurs pour les différents services. L'utilisation de cette interface est décrite plus précisément ci-dessous ( :ref:`interface_datisadmin` )
8. Configuration de la sauvegarde des postes de travail : c'est la phase de mise en route de la sauvegarde sur chaque poste pris en charge
9. Configuration des services supplémentaires en option (selon clients) : les prestations proposées par les revendeurs de la solution Datis peuvent inclure des options qui requiert à leur tour une opération de configuration

.. _pre_requis:

Préparation avant l'installation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Pour éviter toute perte de temps inutile, lors de la venue du technicien pour
l'installation, nous conseillons aux clients qui le peuvent de rechercher ou 
vérifier les éléments suivants, dont le technicien aura besoin:

1. Vérifier que la connexion Internet sur le site d'installation est bien 
de type DSL ou fibre, et dédiée:

- Sauf rare exception, les connexions de type cellulaire (4G/5G) ne sont pas 
  supportées (connexion entrante impossible depuis Internet)

- En cas de connexion partagée (hotel d'entreprise, tiers lieu), informer
  votre revendeur au plus vite, afin qu'il coordonne son intervention
  en amont de sa venue avec l'administrateur réseau de votre site

- Si vous avez souscrit un contrat particulier auprès de l'opérateur Free,
  vous devrez demander à ce dernier l'attribution d'une IP publique dédiée 
  (procédure automatique via `votre console de gestion Free  <https://subscribe.free.fr/login/>`_ )

2. Pensez à un emplacement à l'abri de l'humidité, du soleil, de la poussière
avec une prise réseau et une prise éléctrique (ou informez votre revendeur
en amont de l'installation)

3. L'équipement Inspeere doit impérativement être alimenté par une alimentation
protégée (onduleur, prise HQ). Si vous ne disposez pas d'un tel équipement, 
vérifiez sur votre bon de commande que sa fourniture est bien prévue par le
technicien en charge de l'installation

4. Accès administrateurs. Si l'installation d'une sauvegarde des postes et 
serveurs est prévue, assurez-vous que le technicien aura bien un accès 
administrateur à ces postes, ou mettez-le si besoin en relation avec votre 
prestataire informatique 



.. _interface_datisadmin:

Accès à l'interface de gestion DatisAdmin
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^




