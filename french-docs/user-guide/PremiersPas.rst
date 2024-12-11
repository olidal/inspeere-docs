.. _premiers_pas:

3. Premiers pas, visite guidée
------------------------------

.. _fonctionnement_sauvegarde:

Fonctionnement de la sauvegarde d'Inspeere
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Commençons par expliquer les principes de fonctionnement du système DATIS d'Inspeere.
Le système DATIS, c'est une *appliance*, c'est-à-dire la combinaison d'un équipement 
dédié, un serveur de fichiers, et d'un logiciel très complet. Les deux sont 
indissociables. Par exemple, il n'est pas possible d'installer la partie logicelle de 
DATIS sur un NAS Synology ou QNAP. En revanche, DATIS sait très bien travailler avec 
des NAS. Bien que généralement compact, l'équipement matériel est un vrai serveur (Linux).
Pour certaines configurations musclées, il pourra même prendre la forme d'un serveur
haute performance en rack, et être secondé par une ou plusieurs baies de disque, pour 
atteindre des capacités allant jusqu'à plusieurs Peta-octets. Le système DATIS n'a
aucune limite d'échelle, ce sont vos besoins qui définissent le cahier des charges. 

.. figure:: Image_deux_niveaux_Michael.png
   :width: 720px
   :align: center

   Le système DATIS d'Inspeere comporte deux niveaux.

Comme le montre la figure ci-dessus, le système DATIS d'Inspeere comporte deux niveaux:

- **Niveau service**. Grâce au puissant système de virtualisation *Proxmox*, 
  conçu initialement pour les DataCenter, Datis n'est rien moins qu'un nano-DataCenter.
  Il peut embarquer de nombreux services professionels, et les faire 
  tourner de façon très sure, performante et sécurisée. Lorsqu'un service du niveau 2 
  sauve ses données, celles-ci sont alors enregistrées par le niveau stockage.
   

- **Niveau stockage**. C'est celui qui héberge vos data et celles des autres. 
  Le niveau stockage assure automatiquement et sans ralentissement que les données sont
  journalisées, comprimées, et chiffrées. Les différentes versions restent disponibles
  en cas de besoin (historique), mais sans gaspiller l'espace inutilement. 
  La technologie de pointe qui assure ces opérations n'est autre que le système de 
  fichiers ZFS, que l'on trouve au coeur des équipements de stockage de pointe dans les
  DataCenter ou les gros serveurs, avec des capacités de stockage et d'extension 
  quasi-illimitées. Mais le système DATIS est avant-tout dimensionné en fonction de 
  VOS besoins, ni plus, ni moins, sachant bien sûr que l'espace accordé aux autres ne 
  vous est pas subtilisé. Nous avons simplement doublé l'espace de stockage 
  initial par rapport à vos besoins, pour garantir qu'il ne vous fera jamais défaut;


Maintenant que nous avons vus les deux niveaux, nous pouvons mieux comprendre 
le fonctionnement de la sauvegarde. En fait, DATIS ne propose pas une sauvegarde, 
mais DEUX, une à chaque niveau, comme l'illustre le schema suivant:

.. figure:: Image_deux_niveaux_sauvegarde.png
   :width: 480px
   :align: center

   Les deux niveaux de sauvegarde du système DATIS.

Au niveau du stockage, la technologie unique développée par le CNRS et l'Université 
Côte d'Azur, dont Inspeere exploite le brevet exclusif, permet de sauvegarder vos data
(toujours comprimées et chiffrées) en les découpant d'abord en petit morceaux, puis
en ajoutant de la redondance, pour tolérer les pannes, et enfin en envoyant les morceaux
sur de multiples sites de stockage. 

Cette technologie de dispersion constitue déjà une révolution en matière de 
confidentialité et de sécurité. Mais comme nous sommes aussi très soucieux de 
l'environnement, nous avons choisi d'opérer cette dispersion sur des sites qui 
ne sont pas des DataCenter, mais d'autres utilisateurs de la solution. Le nombre 
de sites choisi, jusqu'a quelques dizaines, est suffisant pour profiter de l'effet 
de groupe, mais tout en restant raisonnable, pour éviter d'impliquer un trop 
grand nombre de destinations.

Entre-elles, le DATIS forment donc de petites communautés de sauvegarde qui 
fonctionnent en vase clos. 

Au niveau du stockage, cette sauvegarde de niveau 1 est ce qui se fait de mieux.
Elle porte sur des objets appelés `volumes` et `datasets` (jargon ZFS). On peut
en définir à loisir autant que l'on veut, le système ZFS n'a AUCUNE limite. Ces 
objets ont chacun une politique de sauvegarde qui lui est propre. 

La politique de sauvegarde permet de définir la durée de retention, la fréquence 
des sauvegardes, et la stratégie d'effeuillement (suppression  des versions 
obsoletes de l'historique), qui peut bien-sûr être progressive. 
Une fois passé le cap de la première sauvegarde, forcément complète, toutes 
les sauvegardes suivantes sont incrémentales, car ZFS les consolide au fur et à 
mesure en offrant la garantie totale d'intégrité du bout en bout quelle que 
soit la durée de vie de l'objet (ZFS vérifie en permanence que les données ne 
sont pas abîmées ou perdues, et corrige automatiquement lorsque cela se produit).

Au dessus de cette sauvegarde de niveau 1 ultra-performante, la sauvegarde des 
postes de travail est un service qui se place au niveau 2, et que nous appelons donc
logiquement, la sauvegarde de niveau 2.

Cette sauvegarde de niveau 2 prend en charge la sauvegarde des postes et serveurs. 
Elle a donc pour objectif de concentrer les data de l'entreprise qui se trouvent 
sur les postes de travail, serveurs, NAS, machines virtuelles et autres baies de 
stockage, vers le système DATIS. Et une fois concentrées sur DATIS, ces données 
issues de la sauvegarde de niveau 2 sont sauvegardées à leur tour au niveau 1 
qui les disperse comme expliqué précédemment.

Ces deux niveaux sont totalement indépendant, ce qui rend le système globalement 
très sûr. D'un point de vue sécurité, par exemple, les deux sauvegardes sont 
"étanches" l'une par rapport à l'autre. En cas de problème au niveau 2, la 
sauvegarde de niveau 1 peut être utilisée pour remettre le système DATIS, ou 
l'un de ses objets de stockage, exactement dans l'état où il se trouvait à une date 
antérieure (par exemple avant une attaque Cyber/Ransomware).

Une différence importante entre les deux niveaux de sauvegarde est que la sauvegarde 
de niveau 2 proposée par defaut par DATIS, est un composant qui peut facilement être 
remplacé ou secondé par un autre.

Par défaut, DATIS propose en effet la solution OpenSource UrBackup, qui offre un
excellent rapport qualité/prix, et répondra brillamment aux besoins de nombreux clients.
Néanmoins, ce choix peut être remis en question sans crainte. Certains de nos clients
préfèrent par exemple utiliser une solution telle que VEEAM, qui est leader sur le 
marché de la sauvegarde de machines virtuelles. La mise en oeuvre d'une solution
complète avec VEEAM au niveau 2 et Datis en externalisation au niveau 1 est 
absolument triviale.


Console de gestion DatisAdmin
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Cette console permet de gérer de façon intuitive et efficace le serveur Urbackup**

.. figure:: ./Figures/1_DatisAdmin_DashBoard_Annot.png
  :width: 480px
  :align: center

  image 1

- Colonne de gauche : Le menu du tableau de bord.
- Au centre : l'état général de l'occupation de l'espace disque disponible.
- En dessous : l'état des machines connectées.


Volumes de partage SMB
^^^^^^^^^^^^^^^^^^^^^^

**Voici comment configurer un lecteur réseau permettant l'accès au partage SMB 
avec un utilisateur.**

Dans l'explorateur de fichier faire un clic droit sur "CePC" puis choisir "Connecter un lecteur réseau"


.. figure:: ./Figures_SMB/SMB_commun2_a.png
  :width: 480px
  :align: center

  image 1


Indiquer ensuite dans la fenêtre le chemin du réseau et le nom utilisateur


.. figure:: ./Figures_SMB/SMB_commun2_aa.png
  :width: 480px
  :align: center

  image 2


Une fenêtre s'ouvre pour vous permettre de vous authentifier



.. figure:: ./Figures_SMB/SMB_commun2_bb.png
  :width: 480px
  :align: center

  image 3


Le lecteur réseau est installé


.. figure:: ./Figures_SMB/SMB_commun2_c.png
  :width: 480px
  :align: center

  image 4


Nextcloud
^^^^^^^^^

.. NOTE::

    Pour Nextcloud aller sur le `site propriétaire <https://www.nextcloud.com>`_
    afin d'avoir toutes les informations nécessaires à l'utilisation de leur produit
    

 


Permissions du dossier COMMUN
"""""""""""""""""""""""""""""

Partage de documents
""""""""""""""""""""

Authentification 2 facteurs
"""""""""""""""""""""""""""

**Dans l'onglet sécurité de la DatisAdmin il est proposé une authentification à double facteur.**

Voici comment procéder:

- Activer le bouton 2FA

.. figure:: ./DATIS_2FA/2FA_1.png
  :width: 480px
  :align: center

  image 1


-Taper son mot de passe dans la fenêtre d'invite.


.. figure:: ./DATIS_2FA/2FA_2.png
  :width: 480px
  :align: center

  image 2


- Flasher le QR Code après avoir pris soin d'installer une application sur son téléphone du type : Google Authenticator

- Pour finir il faut entre le code fourni par cette application dans le champ correspondant (image 3)

.. figure:: ./DATIS_2FA/2FA_3.png
  :width: 480px
  :align: center

  image 3



Réseau privé virtuel (VPN)
""""""""""""""""""""""""""

.. figure:: ./DATIS_VPN/vpn_clé.png
  :width: 480px
  :align: center

  image 1



.. NOTE::

    Pour chaque utilisateur enregistré dans DatisAdmin il est possible d'établir une connexion VPN.
    Il suffit pour cela de cliquer sur la clé correspondant à l'identifiant pour obtenir un fichier de configuration
    VPN. Il faudra également avoir pris soin d'ouvrir le port UDP 1194 dans la console de gestion de votre FAI pour per
    mettre cette connexion.
