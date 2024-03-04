
.. role:: red

2. Configuration du Système DATIS
=================================

Opérations courantes :
* 



2.1 Sauvegardes
---------------

Configuration sauvegarde niveau 1
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _config_client_urbackup:

Configuration sauvegarde niveau 2 : UrBackup
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

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

Interface de gestion centralisée
################################

L'interface de gestion centralisée est accessible depuis l'intranet auquel 
est connecté DATIS, via l'URL ``https://backup.XXXX.inspee.re`` où XXXX 
est l'identifiant à 4 digits hexa de la Datis (cad les 4 derniers digits
de son adresse MAC).

.. figure:: accueil_urbackup.png
   :width: 480px
   :align: center

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

.. _intro_agents_collecte_urbackup:

Agents de sauvegarde
####################

Le client de sauvegarde pour un poste Windows peut-être téléchargé directement 
sur le site UrBackup depuis le poste à sauvegarder, 
`à l'aide de ce lien <https://hndl.urbackup.org/Client/2.4.11/UrBackup%20Client%202.4.11.exe>`_.

Une fois le téléchargement terminé, il suffit de cliquer sur l'exécutable pour
lancer l'installation.

Donnez l'autorisation à l'application d'installation d'apporter des 
 modifications et accepter tous les choix par défaut jusqu'a la fin de l'installation
 
.. figure:: Install_client_privilege.png
   :width: 480px
   :align: center
   
.. figure:: Urbackup_Installer_Bienvenue.png
   :width: 480px
   :align: center

Une fois l'application installée, le menu de configuration s'ouvre automatiquement:

.. figure:: Client_Urbackup_Default_1.png
   :width: 480px
   :align: center

Acceptez les choix par défaut, vous pourrez de toutes façon les changer par
l'interface de supervision de la Datis.

.. warning::
  :strong:`Action requise après chaque installation de client Urbackup`

  Un bug dans l'outil d'installation de la version courante du client Urbackup 
  conduit à une configuration incomplète du pare-feux windows.
  
  Pour éviter toute interruption du service de sauvegarde il est **IMPÉRATIF**
  de :ref:`reconfigurer_le_pare_feu` (sur tous les postes sur lesquels sont déployés 
  les agents Urbackup)

À ce stade deux situations sont possibles:


1. Le client (le poste windows) **EST sur le même subnet que le serveur DATIS**

   Dans ce cas, le client peut fonctionner directement en mode "INTRA-net", 
   qui est le mode par défaut. La configuration du client est alors terminée 
   sur le poste Windows à sauvegarder, car elle pourra éventuellement être 
   modifiée par la suite au niveau de l'interface de gestion.

2. Le client **N'EST PAS sur le même subnet** (par exemple si la DATIS est en DMZ, ou si 
le client est sur un autre site) 

   Dans ce cas, il faut configurer manuellement le client pour un mode de 
   fonctionnement dit "INTER-net". Il reste alors encore une étape de la procédure
   d'association à réaliser sur le poste à sauvegarder, mais cette étape 
   ne pourra être réalisée qu'après avoir lancé la procédure d'association 
   depuis l'interface de gestion centralisée. (décrite au paragraphe suivant). 


.. _intro_procedure_association_urbackup:

Procédure d'association
#######################

UrBackup propose deux formes d'association, qui NE sont PAS exclusives (on peut associer 
un poste Windows des deux façon en même temps):

- association INTRA-net

- association INTER-net

Pour lancer l'une ou l'autre forme, il faut cliquer sur le bouton bleu "Ajouter un client"
sur la page d'accueil de l'interface de gestion.

<Screenshot>


**L'association INTRA-net**:

Comme indiqué sur la copie d'écran suivante, il suffit d'ajouter le nom ou 
l'IP du poste


.. _config_client_timemachine:

Configuration sauvegarde niveau 2 : TimeMachine
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Configuration du client de sauvegarde TimeMachine faisant partie 
du système MacOS, en 6 étapes:


**1. Ouvrir les réglages Time Machine**

.. figure:: ActivationTimeMachine/1-TimeMachineSettings.jpg
  :width: 480px
  :align: center

**2. Ouvrir le menu de sélection des disques TimeMAchine**

.. figure:: ActivationTimeMachine/2-SelectTimeMachineDisk.jpg
  :width: 480px
  :align: center

**3. Sélectionner le disque de votre DATIS**

NB: l'identifiant de la DATIS apparaît à la fin du nom du disque. 
Si vous avez plusieurs DATIS actives sur votre réseau, vous pouvez en sélectionner
plusieurs en recommençant la procédure: votre MAC sauvegardera alternativement
sur chacune des DATIS.

.. figure:: ActivationTimeMachine/3-SelectDisk.jpg 
  :width: 480px
  :align: center


**4. Acceptez la connexion au partage SAMBA de votre DATIS**

.. figure:: ActivationTimeMachine/4-ConnectionTimeMachine.jpg
  :width: 480px
  :align: center

**5. Donnez vos identifiants**

Attention, il s'agit de vos identifiants DATIS, et non pas vos identifiants MAC.
Si vous avez plusieurs MAC à sauvegarder, vous devrez créér autant de comptes
sur DATIS que de MAC.

NB: La procédure de création de comptes DATIS est décrite ici.


.. figure:: ActivationTimeMachine/5-IdentifiantDatisAdmin.jpg
  :width: 480px
  :align: center


**6. C'est fait!**

Vous devez voir le disque ``TimeMachine-XXXX`` dans la liste des disques 
utilisés par TimeMachine, et la première sauvegarde doit commencer bientôt.


.. figure:: ActivationTimeMachine/6-BackupIsRunning.jpg
  :width: 480px
  :align: center


.. _config_VEEAM:

Mise en place sauvegarde niveau 2 : VEEAM
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Sauvegarde Office 365
^^^^^^^^^^^^^^^^^^^^^

Voici en images la procédure de connexion au compte Microsoft 365:

.. figure:: ./Figures_o365/1_connexion_compte.png
  :width: 480px
  :align: center

**Cliquer sur le bouton "connexion"**

.. figure:: ./Figures_o365/2_cjohan.png
  :width: 480px
  :align: center

**Choisir ensuite le nom de connexion**

.. figure:: ./Figures_o365/2_connexion_johan.png
  :width: 480 px
  :align: center

**Une fois celle-ci établie les sauvegardes commencent**


.. figure:: ./Figures_o365/3_onedrive_saves.png
  :width: 480px
  :align: center



.. figure:: ./Figures_o365/4_explorer.png
  :width: 480px
  :align: center

**Il suffit ensuite de choisir le fichier ou dossier à restaurer**


.. sidebar:: [==================================]
  :align: center

2.2 Interface DatisAdmin
------------------------
.. figure:: ./Figures/1_DatisAdmin_DashBoard_Annot.png
  :width: 480px
  :align: center

/figure 1


**1. Tableau de bord de la console d'administration**

 La figure 1 présente le tableau de bord de la console d’administration,
 avec un menu en partie gauche, un rappel de l’état général du système en partie centrale haute,
 et un rappel de l’état de sauvegarde de chaque poste sauvegardé par UrBackup en partie centrale basse.
 Un lien vers la documentation est proposé dans le coin inférieur droit


.. figure:: ./Figures/2_DatisAdmin_2FA_annot.png
  :width: 480px
  :align: center

/figure 2


**2. Chaque utilisateur de la console peut activer une authentification à deux facteurs**

 La console peut-être accessible par différents utilisateurs. Chacun peut activer une authentification à double facteur (figure 2).
 Les utilisateurs créés avec le profile Administrateur ont le droit d’ajouter de nouveaux utilisateur. 
 Les accès des utilisateurs sont centralisés dans une base interne LDAP,
 qui permet d’utiliser les mêmes identifiants pour accéder aux différents services du système INSPEERE Datis.


.. figure:: ./Figures/3_DatisAdmin_Users_Annot.png
  :width: 480px
  :align: center

/figure 3


**3. Le menu de gestion des utilisateurs permet de créer ou modifier des comptes 
utilisateurs et de leur générer des profils VPN Individuels.**

 Le Menu des gestion des utilisateurs (figure 3) permet d’ajouter de nouveaux utilisateurs, de les activer/désactiver, 
 ou de leur délivrer un profile pour établir une connexion VPN (la clé en partie droite). 
 Le profile VPN permet d’accéder aux consoles de gestion et de supervision, ou à certains services trop vulnérables 
 pour être exposés directement sur Internet (SMB, FTP, ...). Initialement, chaque Datis est livrée avec un premier utilisateur « admin »,
 dont les identifiants sont transmis de façon sécurisée à l'administrateur.

.. figure:: ./Figures/4_DatisAdmin_Systeme_General_Annot.png
  :width: 480px
  :align: center

/figure 4

**4. Le menu de gestion du système propose plusieurs onglet de configuration.**

 Le menu de gestion du système (figure 4) permet de configurer ou de consulter les éléments de la configuration système. 
 Nous revenons plus en détail sur les deux derniers concernant les versions et les rapports ci-après.

.. figure:: ./Figures/5_DatisAdmin_Systeme_Version_annot.png
  :width: 480px
  :align: center

/figure 5


**5. Affichage des versions des principaux composants du système, pour une meilleure prise en compte des vulnérabilité potentielles.**

 L’onglet VERSION du menu système (figure 5) permet d’afficher les version actuellement déployées des composants utilisés par le système : 
 version du noyau, du serveur LDAP, VPN, etc. Cette liste permet de vérifier rapidement si le système est vulnérable lors de l’annonce de nouvelles CVE.
 La version courante du système INSPEERE Datis est quant à elle toujours visible en bas à gauche de l’interface DatisAdmin.


.. figure:: ./Figures/6_DatisAdmin_Systeme_Rapports_Annot.png
  :width: 480px
  :align: center

/figure 6


**6. Interface de gestion des Rapports.**

 L’onglet RAPPORTS du menu système (figure 6) permet d’accéder à l’interface de gestion et consultation des rapports de synthèse. 
 Ces rapports sont complémentaires des rapports techniques et alertes mail produits par UrBackup. 
 Ils sont destinés à un public non spécialiste et permettent de vérifier le bon déroulement des sauvegardes de postes.
 Ce menu permet aussi d’activer l’envoi d’un rapport quotidien à une liste d’utilisateurs convenus (par exemple le client final / adhérent).


.. figure:: ./Figures/7_DatisAdmin_Systeme_Rapport_Visu_Annot.png
  :width: 480px
  :align: center

/figure 7


**7. Visualisation d’un rapport.**

 Chaque rapport peut-être soit visualisé sous forme HTML (figure 7), soit téléchargé au format PDF. 
 C’est le même format PDF qui est envoyé par mail lorsque la demande de rapport quotidien est activée.


.. figure:: ./Figures/8_DatisAdmin_Recup_Annot.png
  :width: 480px
  :align: center

/figure 8


**8. La première des deux interfaces de restauration, permet de récupérer des fichiers dans le stockage local 
(fichiers déposés par Samba, Rsync, FTP, etc.)**



 Le menu Récupération (figure 8) permet d’accéder à l’historique de la première des deux formes de sauvegardes, 
 celle des fichiers « déposés » sur le système INSPEERE Datis, 
 à l’aide de protocoles tels que Samba, Rsync, FTP, NFS, etc.

 Le système DATIS prend des instantanés ZFS de l’état du stockage fichier selon la politique de rétention locale planifiée. 
 Cette politique est configurable, avec une granularité variable. Par exemple il est possible de prendre un instantané 
 toutes les 5 minutes pendant 1 heure, puis un toutes les heures pendant 24h, puis un par jour pendant 30j, 
 puis un par semaine pendant 3 mois, etc.

 Une fois l’intervalle de recherche affiné (barre de sélection encadrée en rouge au milieu, figure 8), 
 il suffit de cliquer sur le bouton explorer pour accéder à l’explorateur des instantanés et récupérer le fichier ou dossier voulu. 
 La restitution se fait alors soit en écrasant le contenu actuel, soit a côté en ajoutant la date de l’instantané 
 en suffixe du nom de fichier/dossier. 


.. figure:: ./Figures/9_DatisAdmin_Urbackup_Liste_Annot.png
  :width: 480px
  :align: center

/figure 9


**9. La deuxième interface de restauration est plus spécifiquement dédiée aux sauvegardes de postes et VMs par UrBackup.**

 Le menu Machine Sauvegardées (figure 9) permet d ‘accéder à la deuxième interface de restauration plus spécifiquement dédiée à UrBackup. 
 Elle permet d’obtenir la liste des sauvegardes de postes et VMs gérées par la système UrBackup. Le bouton d’action en bout de ligne permet 
 d’accéder plus spécifiquement aux sauvegardes d’un poste en particulier.
 Il est important de noter que cette interface est complémentaire de l’interface fournie par le système UrBackup. 
 Elle fournit la fonction de restauration granulaire, qui n’est pas disponible autrement par l’interface de UrBackup.

 La restauration granulaire consiste à permettre l’ouverture d’un instantané d’Image disque pour en extraire un fichier. 
 Elle est rendue possible grâce à l’utilisation du backend ZFS avec UrBackup.
 
 Ce backend permet de proposer avec UrBackup une sauvegarde incrémentale perpétuelle, dans laquelle chaque incrément de sauvegarde 
 contient le contenu d’une sauvegarde image complète, mais ne requiert que l’espace supplémentaire d’un incrément. 
 Avec cette forme de sauvegarde, les techniques de sauvegardes complètes,  « full synthetique », ou incrémentales inversée 
 deviennent totalement inutiles : l’espace disque occupé est minimal, et il est possible de réduire le nombre d’instantanés 
 en supprimant n’importe le(s)quel(s), en fonction des objectifs de la politique de rétention.


.. figure:: ./Figures/10_DatisAdmin_Urbackup_ListeOne.png
  :width: 480px
  :align: center

/figure 10


**10. Navigation dans les sauvegardes images UrBackup d’un poste en particulier.**

 En cliquant sur le bouton d’action à fin de la ligne correspondant à un poste sauvegardé (figure 9), 
 on obtient la liste des sauvegardes de type image et de type fichier de UrBackup. Pour chaque instantané de sauvegarde de type image, 
 il est possible d’ouvrir une nouvelle  page de détails spécifique à cet instantané (bouton action en fin de ligne sur la figure 10).


.. figure:: ./Figures/11_DatisAdmin_UrBackup_ExploreImg_Annot.png
  :width: 480px
  :align: center

/figure 11


**11.Ouverture d’un instantané de volume du poste sauvegardé.**

 Lorsque le volume explorer correspond à une partition d’origine (disque C, D, ...), il est possible de « monter » l’image 
 afin d’accéder à son contenu (figure 11). Il est alors possible d’explorer le contenu de l’image et d’en télécharger 
 des fichier à l’aide des boutons d’action en fin de ligne.

 Il est important de noter que toute cette séquence d’ouverture est très rapide, car grâce au stockage ZFS, 
 l’accès au contenu d’un instantané ne requiert aucune phase de reconstruction/consolidation : en pratique, 
 chaque instantané est une sauvegarde complète, immédiatement disponible.

Tableau de bord de supervision centralisé
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. figure:: ./Figure_Graf/1_Etat_global_Grafana_Annot.png
  :width: 480px
  :align: center

/figure 1

**1. La zone supérieure du tableau de bord présente un « cartouche » par serveur. Chaque cartouche est une matrice 3x2 d’indicateurs de couleur. 
La zone suivante offre un niveau de détail plus élevé. Elle constituée d’une série de lignes d’indicateurs, les « one-liner », une pour chaque serveur.**

 


 La figure 1 montre la partie haute du tableau de bord. Tout en haut, on trouve la zone des « cartouches » qui présente de façon compacte 
 l’état de chaque serveur, à l’aide de 6 indicateurs, organisés en matrice 3x2. Le code couleur est intuitif : 
 vert quand tout va bien, bleu quand un indicateur est sans objet (par exemple lorsque la sauvegarde UrBackup de type fichier n’est pas utilisée), 
 et jaune, puis orange, puis rouge en fonction du niveau d’alerte. Dans le cas présent, les cases oranges indiquent que des sauvegardes UrBackup 
 de type fichier ou image sont en retard sur 3 des 4 serveurs.

 Vient ensuite la zone des « one-liners » qui donne un peu plus d’information sur l’état du stockage ZFS local et distant, 
 pour chaque serveur, sur une ligne par serveur (cadre rouge en partie basse de la figure 23).


.. figure:: ./Figure_Graf/2_Etat_Systeme_Annot.png
  :width: 480px
  :align: center

/figure 2

**2. En faisant défiler la page vers le bas, on atteint la zone centrale du tableau de bord, avec les indicateurs système de chaque serveur.
Ici la figure présente les indicateurs pour un serveur. Il faut faire défiler la page pour obtenir les même indicateurs avec les serveurs suivants.**

 La figure 2 montre la zone des indicateurs système d’un serveur. A coté des indicateurs classique de charge et d’occupation mémoire, 
 on trouve les indicateurs concernant l’état du stockage primaire ZFS. La aussi le code couleur est conservé : lorsque c’est vert (ONLINE), 
 le stockage n’a pas d’erreur. Si un disque venait à perdre des secteur, l’état passerait en orange (DEGRADED), et en cas de défaillance grave, 
 il passe en rouge (FAULTED). La quantité de stockage libre/utilisé est aussi un indicateur important à surveiller 
 (2e cadre rouge en partant du haut, dans la figure 13). Enfin, tout en bas de cette zone système, on trouve la courbe du trafic de sauvegarde, 
 avec des couleurs différentes pour le trafic en provenance des postes sauvegardés, et celui à destination des réplicats externes.


.. figure:: ./Figure_Graf/3_Etat_Urbackup_Annot.png
  :width: 480px
  :align: center

/figure 3

**3. En faisant encore défiler jusqu’en bas de la page du tableau de bord, on atteint la zone concernant l’état des sauvegardes UrBackup
sur chacun des serveurs. Les informations présentées sont les même que celles présentées sur la console UrBackup, mais regroupées
en un seul et même endroit pour tous les serveurs Datis d’un même client ou tous les client d’un même partenaire.**



Gestion des utilisateurs
^^^^^^^^^^^^^^^^^^^^^^^^

Fonctions système
^^^^^^^^^^^^^^^^^

Récupération d'un fichier dans sauvegarde niveau 1
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

2.3 Serveur de fichiers (SMB)
-----------------------------

Types de Partages
^^^^^^^^^^^^^^^^^

Partages avec sauvegardes
^^^^^^^^^^^^^^^^^^^^^^^^^

Partages et Nextcloud
^^^^^^^^^^^^^^^^^^^^^

2.4 Option Nextcloud
--------------------

Fonctionalités par défaut
^^^^^^^^^^^^^^^^^^^^^^^^^

Espace de partage (dossier COMMUN)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
