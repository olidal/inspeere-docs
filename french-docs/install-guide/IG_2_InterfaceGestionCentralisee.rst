2. InterfaceGestionCentralisee
==============================


La sauvegarde des postes de travail, serveurs et machines virtuelles windows
est assurée à l'aide de l'outil UrBackup (documentation: `EN <https://www.urbackup.org/>`_ |
`FR <https://www-urbackup-org.translate.goog/?_x_tr_sl=en&_x_tr_tl=fr&_x_tr_hl=fr-FR>`_).


.. panels::
  :header: text-center
  :column: col-lg-12

  A propos du choix de l'outil UrBackup
  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

  Urbackup est un outil issu du monde OpenSource.

  Il a été choisi pour son niveau de maturité (le projet existe et est activement
  maintenu depuis plus de 10 ans) et ses performances lors des phases de
  sauvegarde et de restauration.


.. _intro_interface_gestion_urbackup:

**Interface de gestion centralisée**


L'interface de gestion centralisée est accessible depuis l'intranet auquel
est connecté DATIS, via l'URL ``https://backup.XXXX.inspee.re`` où XXXX
est l'identifiant à 4 digits hexa de la Datis (cad les 4 derniers digits
de son adresse MAC).

.. figure:: accueil_urbackup.png
  :width: 480px
  :align: center

  image 1

Le mot de passe pour accéder à cette interface est généré automatiquement
lors de l'activation et transmis:

- soit par Inspeere au technicien en charge de l'installation

- soit reçu directement par le partenaire Inspeere lors de l'activation
  du contrat

Contacter le `support Inspeere <mailto:support@inspeere.com>`_ si ce
code n'a pas été reçu.


Certains réglages de l'interface de gestion sont automatiquement préconfigurés
par le système DATIS:

- configuration mail sortant (pour recevoir les notifications et alertes)

- plan de sauvegarde en mode fichier

- plan de sauvegarde en mode image

Suivant la philosophie DATIS, la sauvegarde est donc en état de fonctionner
dès l'ajout des premiers clients. Il est néanmoins toujours possible de modifier
les réglages par défaut via l'onglet des réglages.


.. figure:: reglages_urbackup.png
  :width: 480px
  :align: center

  image 2

.. _intro_agents_collecte_urbackup:
