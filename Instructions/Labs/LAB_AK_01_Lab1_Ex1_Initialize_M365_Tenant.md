## Locataires WWL - Conditions d’utilisation

Si un locataire vous est fourni dans le cadre d’une formation dispensée par un instructeur, notez qu’il est mis à votre disposition dans le seul but de prendre en charge les labos pratiques de la formation. 

Vous ne devez ni partager ni utiliser les locataires en dehors des labos pratiques. Le locataire utilisé dans ce cours est un locataire d’essai. Au terme de la classe, le locataire ne pourra pas faire l’objet d’une prolongation et vous ne pourrez plus l’utiliser ni y accéder. 

Vous n’êtes pas autorisé à convertir un locataire en abonnement payant. Les locataires obtenus dans le cadre de ce cours sont la propriété de Microsoft Corporation. Nous nous réservons le droit d’y accéder et d’en reprendre possession à tout moment. 

# Parcours d’apprentissage 1 : Labo 1 – Exercice 1 – Initialiser votre locataire Microsoft 365 

Adatum Corporation est une filiale de Contoso Electronics. Adatum exécute ses applications héritées (comme Microsoft Exchange Server 2019) dans un déploiement local. Toutefois, il s’est récemment abonné à Microsoft 365, créant ainsi un déploiement hybride dans lequel il doit synchroniser ses déploiements locaux et cloud. 

En tant qu’administrateur Microsoft 365 d’Adatum, vous avez été chargé de déployer Microsoft 365 dans le déploiement hybride d’Adatum à l’aide d’un environnement lab virtualisé. Dans cet exercice, vous allez configurer le locataire d’évaluation gratuite Microsoft 365 d’Adatum et votre instructeur vous expliquera comment obtenir vos informations d’identification Microsoft 365 dans votre environnement hébergé dans un labo. Vous allez utiliser ces informations d’identification dans les labos restants de ce cours. 

Dans votre environnement de labo, le fournisseur d’hébergement de votre labo a déjà obtenu un tenant d’évaluation gratuite Microsoft 365 pour vous. Le fournisseur de votre labo a déjà créé deux comptes administrateur que vous allez utiliser dans l’environnement de labo de votre machine virtuelle : 

- Un compte d’administrateur AD DS pour l’environnement local d’Adatum (Adatum\Administrator).
- Un compte administrateur de locataire par défaut dans Microsoft 365 (le nom d’affichage pour ce compte d’utilisateur est Administrateur MOD). 

Vous allez vous connecter au PC Client 1 (LON-CL1) en utilisant le compte Adatum\Administrator. Lorsque vous accédez à Microsoft 365 pour la première fois, vous vous connectez initialement en utilisant le compte administrateur de locataire Microsoft 365 (Administrateur MOD). Vous allez ensuite mettre à jour le profil d’organisation Microsoft 365 d’Adatum, puis préparer votre locataire pour Microsoft Entra ID et pour les labos ultérieurs à l’aide de la Gestion des droits relatifs à l’information, des alertes d’audit et de Microsoft Graph PowerShell.


### Tâche 1 - Connectez-vous au Centre d’administration Microsoft 365.

Tout au long des labos de ce cours, vous allez jouer le rôle du personnage nommé Holly Dickson, l’administrateur Microsoft 365 d’Adatum. Dans le cadre de votre rôle en tant qu’Holly, vous vous chargez de la configuration du profil de l’entreprise pour son locataire d’évaluation gratuite Microsoft 365. Dans cette tâche, vous allez configurer les options nécessaires pour un locataire d’Adatum. Étant donné qu’Holly n’a pas encore créé de compte d’utilisateur personnel Microsoft 365 pour elle-même (vous l’effectuerez dans l’exercice de labo suivant), Holly se connecte initialement à Microsoft 365 en utilisant le compte administrateur de locataire et le mot de passe Microsoft 365 par défaut créés par le fournisseur d’hébergement de votre labo. Ce compte constitue le compte Administrateur MOD dont l’alias est « admin ». Le nom d’utilisateur pour ce compte est admin@xxxxxZZZZZZ.onmicrosoft.com (où xxxxxZZZZZZ est le préfixe de locataire attribué par le fournisseur d’hébergement de votre labo). Le nom d’affichage pour ce compte est Administrateur MOD.

1. Votre fournisseur d’hébergement de laboratoire fournit deux mots de passe utilisés avec les comptes d’utilisateur fictifs dans votre locataire d’évaluation Microsoft 365. Le compte Administrateur MOD, qui est l’administrateur de locataire par défaut, a reçu le **mot de passe d’administration**. Tous les autres utilisateurs , même ceux affectés à un rôle d’administrateur, ont été affectés au **mot de passe de l’utilisateur**. <br>

    À des fins de sécurité, Microsoft a configuré votre locataire d’évaluation afin que tous les utilisateurs prédéfinis puissent modifier leur mot de passe lors de leur prochaine connexion. <br>
 
    **Important :** certains fournisseurs d’hébergement de labo peuvent fournir les nouveaux champs de mot de passe suivants qui seront utilisés pour stocker les nouveaux mots de passe que vous affecterez aux utilisateurs la première fois qu’ils se connectent : <br>

    - **Nouveau mot de passe d’administration** - Il s’agit du nouveau mot de passe que vous allez affecter à l’administrateur MOD et à Holly Dickson.
    - **Nouveau mot de passe utilisateur ** - Il s’agit du nouveau mot de passe que vous affecterez à tous les autres utilisateurs.

    Si ces deux nouveaux champs de mot de passe apparaissent dans votre machine virtuelle, entrez un nouveau mot de passe pour chacun d’eux. Ces nouvelles valeurs de mot de passe seront stockées dans la machine virtuelle et affichées dans les instructions du labo. <br>
 
    D’autres fournisseurs d’hébergement de laboratoire peuvent ne pas fournir ces nouveaux champs de mot de passe. Pour ces environnements, vous devez écrire manuellement le nouveau mot de passe que vous prévoyez d’affecter aux utilisateurs qui se connectent. <br>

    Lorsque vous concevez vos nouveaux mots de passe, gardez à l’esprit les instructions de mot de passe de Microsoft : <br>

    - Longueur minimale de 8 caractères, avec au moins :
       - 1 caractère majuscule
       - 1 caractère minuscule
       - 1 caractère spécial. Les mots de passe ne seront pas validés par rapport aux exigences de Microsoft tant que vous ne modifiez pas l’ancien mot de passe lors de la prochaine connexion de l’utilisateur.

3. Lorsque vous ouvrez l’environnement de machine virtuelle du fournisseur d’hébergement de votre labo, vous devez commencer par la Machine virtuelle Client 1 (LON-CL1). Si votre environnement de machine virtuelle s’ouvre avec l’une des autres machines (telle que LON-DC1), basculez maintenant vers **LON-CL1**.

4. Connectez-vous à **LON-CL1** avec le compte **Administrateur** créé par votre fournisseur d’hébergement de labo avec le mot de passe **Pa55w.rd**. 

5. Dans la barre des tâches en bas de votre écran, sélectionnez l’icône **Microsoft Edge**. Si nécessaire, agrandissez la fenêtre de votre navigateur quand elle s’ouvre.

6. Dans votre navigateur Edge, accédez à la page **Accueil Microsoft 365** en entrant l’URL suivante dans la barre d’adresse : **https://portal.office.com** 

7. Dans la boîte de dialogue **Se connecter**, entrez le nom **d’utilisateur administratif** fourni par votre fournisseur d’hébergement lab (il s’agit du compte Administrateur MOD) de votre locataire d’évaluation Microsoft 365. Le nom d’utilisateur doit se présenter sous la forme **admin@xxxxxZZZZZZ.onmicrosoft.com**, où xxxxxZZZZZZ est le préfixe de locataire attribué par le fournisseur d’hébergement de votre labo. Cliquez sur **Suivant**. <br/>

    **Remarque :** Dans les instructions du labo s’affichant dans votre environnement de laboratoire de machine virtuelle, le fournisseur d’hébergement de votre labo peut offrir la possibilité de sélectionner un bouton **Saisir un texte** (ou équivalent) près des données de ressource, comme les noms d’utilisateur, les mots de passe, les commandes PowerShell et d’autres données devant être entrées pendant ces labos. D’autres fournisseurs d’hébergement de labo peuvent offrir une autre méthode, comme la possibilité de copier et de coller ces informations. Tirez parti de cette fonctionnalité pour vous éviter d’avoir à saisir manuellement ces informations. 

8. Dans la boîte de dialogue **Entrer le mot de passe**, entrez le **mot de passe d’administration** prédéfini fourni par votre fournisseur d’hébergement lab, puis sélectionnez **Se connecter**. 

9. Votre fournisseur d’hébergement lab peut ou non avoir configuré le compte d’administrateur MOD pour exiger un nouveau mot de passe lors de la connexion. Si c’est le cas, une boîte de dialogue **Mettre à jour votre mot de passe** s’affiche. Si cela se produit, entrez le **mot de passe d’administration** fourni par votre fournisseur d’hébergement de labo dans le champ **Mot de passe actuel**, puis entrez le nouveau mot de passe d’administration dans les champs **Nouveau mot de passe** et **Confirmer le mot de passe**.

10. Si une boîte de dialogue **Rester connecté ?** s’affiche, cochez la case **Ne plus afficher**, puis sélectionnez **Oui**. 

11. Si une boîte de dialogue **Bienvenue dans Microsoft 365** s’affiche au milieu de l’écran, il n’existe aucune option pour la fermer. Au lieu de cela, à droite de la fenêtre, sélectionnez deux fois l’icône de flèche vers l’avant (**>**), puis sélectionnez l’icône de coche pour parcourir les diapositives de cette fenêtre de message. 

12. Si une boîte de dialogue **Rechercher d’autres applications** ou une boîte de dialogue **Créer avec Microsoft 365** s’affiche, sélectionnez le **X** dans le coin supérieur des zones pour les fermer. De même, si une boîte de dialogue Se connecter à Microsoft Edge s’affiche, sélectionnez le bouton **Non merci**.

13. La page **Bienvenue dans Microsoft 365** s’affiche dans votre navigateur Edge sous l’onglet **Accueil | Microsoft 365**. Il s’agit de la page d’accueil Microsoft 365 de l’Administrateur MOD. <br/>

    Notez qu’une icône ou un cercle avec « MA » (initiales pour l’administrateur MOD) apparaît dans le coin supérieur droit de l’écran. Certains locataires d’évaluation affichent une icône ; d’autres montrent les initiales « MA » dans un cercle ; tout dépend du fait que votre fournisseur d’hébergement de laboratoire a ajouté une icône au compte de l’administrateur MOD. L’icône ou les initiales représentent le compte **administrateur MOD**, qui est le compte d’administrateur client créé par votre fournisseur d’hébergement lab que vous venez de vous connecter en tant que. Si l’un des comptes d’utilisateur Microsoft 365 existants créés par votre fournisseur d’hébergement lab a une image associée à son compte, l’image de l’utilisateur s’affiche plutôt que les initiales de l’utilisateur lorsque vous vous connectez à Microsoft 365 en tant qu’utilisateur. Toutefois, lorsqu’un utilisateur tel que l’administrateur MOD n’a aucune image affectée à celui-ci, les initiales de l’utilisateur sont affichées à la place de l’image, ou une icône s’affiche si un utilisateur a été affecté au compte par votre fournisseur d’hébergement lab. <br/>

    Dans la page **Bienvenue dans Microsoft 365**, dans la liste des icônes d’application qui s’affiche dans le volet de navigation, sélectionnez **Administrateur**. Cela ouvre le **Centre d’administration Microsoft 365** dans un nouvel onglet de navigateur. 

14. Dans le **centre d’administration Microsoft 365**, dans le volet de navigation, sélectionnez **Afficher tout**. Cela affiche toutes les options de navigation pour le Centre d’administration Microsoft 365.

15. Restez connecté à **LON-CL1** avec Microsoft Edge ouvert dans le **Centre d’administration Microsoft 365** pour la tâche suivante.

### Tâche 2 : créer un thème personnalisé pour une équipe du projet pilote d’Adatum

Dans la tâche précédente, vous avez appris que lorsqu’un utilisateur est connecté à Microsoft 365, le système affiche sa photo (s’il en a fourni une) ou ses initiales dans le cas contraire. Holly Dickson, l’Administrateur Microsoft 365 d’Adatum, ne se satisfait pas de voir simplement la photo ou les initiales de l’utilisateur connecté. Elle souhaite créer un thème personnalisé pour les membres de l’équipe de son projet pilote afin qu’il affiche également le nom de l’utilisateur connecté. Si les membres de l’équipe préfèrent cette conception à la fin du projet pilote, elle configurera cette même option dans le thème par défaut afin qu’elle s’applique à tous les utilisateurs. 

Les thèmes personnalisés doivent être associés à un ou plusieurs groupes Microsoft 365. Par conséquent, Holly doit d’abord créer un groupe Microsoft 365 pour tous les membres de l’équipe du projet pilote afin d’implémenter cette modification. Elle peut également créer un thème personnalisé associé à ce groupe qui permet au paramètre d’afficher le nom d’utilisateur connecté. Dans cette tâche, vous allez créer un groupe Microsoft 365 pour les membres de l’équipe du projet pilote Microsoft 365. Vous allez ensuite créer un thème personnalisé qui affiche le nom d’utilisateur connecté et attribuer ce thème à l’équipe du projet pilote. Vous allez également passer en revue d’autres options que vous pouvez configurer avec des thèmes personnalisés. Vous pouvez également apporter tous les changements de couleur de votre choix.

**Important :** À la fin de cette tâche, vous tenterez d’enregistrer le thème personnalisé que vous avez créé. Il existe un problème de plateforme connu dans le centre d’administration Microsoft 365, qui enregistre parfois le thème personnalisé correctement, et qui d’autres fois retourne un message indiquant « Désolé, nous n’avons pas pu enregistrer votre thème. Veuillez réessayer plus tard. » Si vous recevez ce message, il n’y a rien à faire, passez à autre chose. Essayer d’enregistrer le thème ultérieurement retourne généralement la même erreur. Ce problème n’affecte pas les labos futurs, sauf que le nom de l’utilisateur ne s’affichera pas en regard de son icône d’utilisateur, ni les initiales sur la ligne de titre. Malgré ce problème connu, nous voulons toujours que vous effectuiez cette tâche pour acquérir de l’expérience dans la création d’un thème, même s’il se peut qu’il ne soit pas enregistré dans votre locataire d’évaluation.

1. Vous devriez toujours être connecté à LON-CL1 avec le compte **adatum\administrator**, et dans votre navigateur Edge, vous devriez toujours être connecté à Microsoft 365 en tant qu’**Administrateur MOD**. 

2. Dans le **Centre d’administration Microsoft 365**, sélectionnez **Équipes + groupes** dans le volet de navigation et, en dessous, sélectionnez **Équipes et groupes actifs**. 

3. Dans la page **Équipes et groupes actifs** figure un onglet permettant d’afficher chacun des types de groupes. L’onglet **Groupes Microsoft 365 et Teams** est affiché par défaut. Cet onglet affiche les groupes Microsoft 365 existants.  <br/>

    Sélectionnez l’option **+ Ajouter un groupe Microsoft 365** qui s’affiche dans la barre de menus au-dessus de la liste des Groupes Microsoft 365 et Teams. Cette option lance l’Assistant **Ajouter un groupe Microsoft 365**. 

4. Dans l’Assistant **Ajouter un groupe Microsoft 365** de la page **Configurer les éléments de base**, entrez **Projet pilot M365** dans le champ **Nom**, puis **Membres de l’équipe du projet pilote Microsoft 365** dans le champ **Description** (remarque : même si vous n’entrez aucune description, vous devez toujours sélectionner ce champ pour activer le bouton **Suivant**). Cliquez sur **Suivant**.

5. Vous allez maintenant attribuer l’Administrateur MOD en tant que propriétaire du groupe **projet pilote M365**. Dans la fenêtre **Attribuer des propriétaires**, sélectionnez **+ Attribuer des propriétaires**.
    
6. Dans le volet **Attribuer des propriétaires** qui s’affiche, sélectionnez la case à cocher près de **Administrateur MOD**, puis le bouton **Ajouter (1)** en bas du volet.

7. Dans la page **Attribuer des propriétaires**, l’Administrateur MOD doit s’afficher comme propriétaire du groupe. Cliquez sur **Suivant**.

8. Vous allez maintenant attribuer des membres au groupe de projet pilote M365. Dans la page **Ajouter des membres**, sélectionnez **+ Ajouter des membres**.

9. Dans le volet **Ajouter des membres** qui s’affiche, sélectionnez les cases à cocher près des utilisateurs suivants (dans l’ordre alphabétique) : **Alex Wilber**, **Allan Deyoung**, **Diego Siciliani**, **Isaiah Langer**, **Joni Sherman**, **Lynne Robbins**, **Megan Bowen**, **Administrateur MOD**, **Nestor Wilke** et **Patti Fernandez**. Ensuite, sélectionnez le bouton **Ajouter (10)** en bas du volet.

10. Dans la page **Ajouter des membres**, vérifiez que ces 10 utilisateurs sont répertoriés comme membres du groupe. Si un utilisateur est manquant, sélectionnez **+ Ajouter des membres**, puis ajoutez l’un des 10 utilisateurs manquants. Quand tous les 10 utilisateurs s’affichent dans la page, sélectionnez **Suivant**.

11. Dans la page **Modifier les paramètres**, entrez les informations suivantes : <br/>

    - Entrez **m365pilotproject** dans le champ **Adresse e-mail du groupe**.
    - Dans le champ **Confidentialité**, sélectionnez **Privé**.
    - Sous la section **Ajouter Microsoft Teams à votre groupe**, vérifiez que la case à cocher **Créer une équipe pour ce groupe** est sélectionnée (sélectionnez-la si elle est vide), puis sélectionnez **Suivant**.

12. Dans la page **Vérifier et terminer l’ajout d’un groupe**, passez en revue le contenu saisi. Si vous devez corriger un élément, sélectionnez **Modifier** sous la zone spécifique nécessitant un ajustement, apportez les corrections nécessaires, puis sélectionnez **Suivant** afin de poursuivre sur cette page. Une fois que tout est correct, sélectionnez **Créer un groupe**.

13. Une fois que la fenêtre **Groupe de projet pilot M365 créé** s’affiche, notez le commentaire en haut de la page indiquant que l’affichage du nouveau groupe dans la liste des groupes actifs peut prendre 5 minutes.  </br>

    Sélectionnez **Fermer**. Cette option vous fait revenir à la page **Équipes et groupes actifs** dans laquelle l’onglet **Groupes Microsoft 365 et Teams** doit s’afficher. Étant donné que le groupe du projet pilote M365 était un groupe Microsoft 365, il doit finir par s’afficher sous cet onglet. Le cas échéant, sélectionnez l’option **Actualiser** sur la barre de menu jusqu’à ce que vous voyiez le groupe du projet pilote M365 dans la liste des Groupes Microsoft 365 et Teams.

14. Dans le **centre d’administration Microsoft 365**, sélectionnez **Paramètres** dans le volet de navigation, puis **Paramètres de l’organisation**. 

15. Sur la page des **paramètres de l'organisation**, l'onglet **Services** s'affiche par défaut. Sélectionnez l’onglet **Profil d’organisation**.

16. L’onglet **Profil de l’organisation** affiche la liste des données de profil de l’organisation. Dans la liste des données, sélectionnez **Thèmes personnalisés**.

17. Dans le volet **Personnaliser Microsoft 365 pour votre organisation** qui s’affiche, vous pouvez personnaliser le thème par défaut visible par les utilisateurs connectés à Microsoft 365 ou ajouter d’autres thèmes personnalisés. Vous souhaitez créer un thème personnalisé qui s’applique uniquement aux membres du groupe **Projet pilote M365** que vous avez créé précédemment. Sélectionnez l’option **+Ajouter un thème**.

18. Dans le volet **Nouveau thème de groupe** qui s’affiche, l’onglet **Général** s’affiche par défaut. Entrez **Thème de projet pilote M365** dans le champ **Nom**.

19. Cliquez à l’intérieur du champ **Groupes**. Dans la liste de groupes qui s’affiche, sélectionnez **Projet pilote M365** s’il s’affiche dans celle-ci. <br/>

    **Remarque :** Si **Projet pilote M365** ne s’affiche pas dans la liste de groupes, entez **M365** dans le champ **Groupes**. Une zone des résultats de la recherche doit s’afficher et montrer le groupe **Projet pilote M365**. Sélectionnez **Projet pilote M365**. 

20. Sélectionnez la case à cocher **Afficher le nom d’affichage de l’utilisateur**. Il s’agit du paramètre qu’Holly souhaite personnaliser pour les membres de l’équipe du projet pilote M365. Cette option affiche le nom de l’utilisateur connecté à côté de ses initiales dans chaque titre de fenêtre.
 
21. Sélectionnez l’onglet **Logos** et prenez le temps de passer en revue ses options. Faites de même pour l’onglet **Couleurs**. Notez les différentes options de thème et de personnalisation disponibles que vous pouvez mettre à jour. <br/>

    Dans le cadre de ce labo, vous pouvez modifier l’une des options ou laisser les valeurs par défaut telles quelles. Par exemple, dans votre environnement réel, vous pouvez ajouter le logo de votre entreprise et définir l’image d’arrière-plan comme valeur par défaut pour tous vos utilisateurs. Pour ce labo, n’hésitez pas à modifier les couleurs de votre volet de navigation, la couleur de texte, la couleur d’icône et la couleur d’accentuation. <br/>

    **Explorez les différentes options de ce thème qui sera utilisé par les membres de l’équipe Projet pilote Microsoft 365. Apportez les modifications souhaitées.** <br/>

    **Conseil :** Certains motifs de couleur peuvent distraire les utilisateurs. Si vous modifiez l’une des couleurs, il est recommandé d’éviter d’utiliser des couleurs à contraste élevé ensemble, telles que des couleurs néon et des couleurs haute résolution comme rose vif et blanc.

22. Sélectionnez **Enregistrer**. 

    **Remarque :** Comme mentionné précédemment au début de cette tâche, il existe un problème de plateforme connu dans le centre d’administration Microsoft 365 qui enregistre parfois un nouveau thème personnalisé, et qui d’autres fois retourne un message indiquant « Désolé, nous n’avons pas pu enregistrer votre thème. Veuillez réessayer plus tard. » Si vous recevez ce message, cela n’affectera pas les labos futurs. Étant donné que votre thème personnalisé n’a pas été enregistré, le système n’affiche simplement pas le nom de l’utilisateur en regard de son icône d’utilisateur ou ses initiales sur la ligne de titre (les modifications de couleur que vous avez apportées n’apparaîtront pas non plus). Nous vous avons toujours demandé d’effectuer cette tâche, même si vous pouvez recevoir ce message, afin que vous puissiez acquérir l’expérience de création d’un thème tel que celui-ci. Par conséquent, si vous obtenez cette erreur, ignorez l’étape suivante, qui teste le thème personnalisé. Toutefois, vous pouvez toujours effectuer les étapes restantes après l’étape suivante pour en savoir plus sur le thème par défaut. Que votre thème personnalisé ait été enregistré ou non, fermez le volet **Thème Projet pilote M365**.

23. Si votre thème personnalisé n’a pas été enregistré, passez à l’étape suivante. Toutefois, si votre thème personnalisé a été enregistré, sélectionnez l’icône **Actualiser** en haut de l’écran, à gauche de la barre d’adresses. Une fois l’écran actualisé, observez la façon dont le nom **Administrateur MOD** s’affiche à côté du cercle avec les initiales AM, ou de l’icône sélectionnée pour ce compte par votre fournisseur d’hébergement de labo. Lorsque les membres de l’équipe Projet pilote Microsoft 365 se connectent à Microsoft 365, ce thème personnalisé affiche son nom d’utilisateur, tout comme le nom Administrateur MOD apparaît ici. 

24. Dans les données du profil de l’organisation, sélectionnez **Thèmes personnalisés**.

25. Dans le volet **Personnaliser Microsoft 365 pour votre organisation** qui s’affiche, notez l’affichage du **Thème par défaut** et du **Thème Projet pilote M365** (si le thème a été enregistré à l’étape précédente). Sélectionnez le **Thème par défaut**. 

26. Dans le volet **Thème par défaut**, notez que l’option **Afficher le nom d’affichage de l’utilisateur** n’est pas sélectionnée pour le thème par défaut. Si Holly décide plus tard de transformer l’option **Afficher le nom d’affichage de l’utilisateur** en fonctionnalité permanente, elle sélectionnera cette option dans le volet **Thème par défaut** pour qu’elle s’applique à tous les utilisateurs Adatum et supprimera le **Thème du projet pilote M365**. <br/>

    **Remarque :** Si vous avez reçu le message « Désolé, nous n’avons pas pu enregistrer votre thème. » Veuillez réessayer plus tard. » lorsque vous avez précédemment essayé d’enregistrer votre thème personnalisé, sélectionnez l’option **Afficher le nom d’affichage de l’utilisateur** sur le thème par défaut, puis sélectionnez **Enregistrer**. Nous voulons que vous voyiez ce qui se passe quand cette option est sélectionnée, même si vous n’avez pas pu enregistrer votre thème personnalisé. Si vous définissez cette option sur le thème par défaut, sélectionnez l’icône **Actualiser** en haut de l’écran, à gauche de la barre d’adresses. Une fois l’écran actualisé, notez comment le nom **Administrateur MOD** apparaît à gauche du cercle avec les initiales AM ou l’icône sélectionnée pour ce compte par votre fournisseur d’hébergement de labo.
 
27. Fermez le volet **Thème par défaut**.

28. Restez connecté à **LON-CL1** avec Microsoft Edge ouvert dans le **Centre d’administration Microsoft 365** pour la tâche suivante.


### Tâche 3 : installer Microsoft Graph PowerShell 

Microsoft Graph PowerShell est nécessaire pour effectuer plusieurs tâches de configuration lors de l’installation de Microsoft 365. Étant donné que de futurs exercices de labo vont effectuer plusieurs de ces tâches en tirant parti de Windows PowerShell, vous devez commencer par installer le module Microsoft Graph PowerShell. Ce module vous permet d’effectuer plusieurs des tâches d’administration d’organisation et d’utilisateur Microsoft 365 via PowerShell. Il est idéal pour des tâches en bloc comme les réinitialisations de mots de passe, les stratégies de mots de passe, la gestion des licences et la création de rapports, etc.  

1. Sur LON-CL1, vous devriez toujours être connecté avec le compte **adatum\administrator**. Pour installer Microsoft Graph PowerShell, vous devez ouvrir une instance élevée de **Windows PowerShell**. Cliquez avec le bouton droit sur l’icône **Windows (Démarrer)** dans le coin en bas à gauche de la barre des tâches, puis sélectionnez **Windows PowerShell (Admin)**.

2. Agrandissez votre fenêtre PowerShell. Dans **Windows PowerShell**, tapez la commande suivante lors de l’invite de commandes pour installer le module Microsoft Graph PowerShell à partir de PowerShell Gallery, puis appuyez sur Entrée : <br/>

        Install-Module Microsoft.Graph -Scope CurrentUser

3. Vous allez être invité à confirmer que vous souhaitez installer le module à partir d’un référentiel non approuvé (PSGallery). Entrez **Oui** pour sélectionner **[A] Oui pour tout**, puis appuyez sur Entrée.  <br/>

    **Remarque :** Votre réponse va lancer l’installation de tous les sous-modules de Microsoft Graph. Une fois l’affichage terminé des messages d’installation pour chaque sous-module, l’installation complète de Microsoft Graph PowerShell prend entre 5 et 10 minutes de plus. Pendant ce temps, le curseur continuer de clignoter sous le message de référentiel non approuvé. <br/>

    **Cela peut être le bon moment de faire une courte pause.**

4. Une invite de commandes s’affiche après l’installation de Microsoft Graph PowerShell. La liste des sous-modules installés s’affiche désormais. Pour cela, exécutez la commande suivante :

        Get-InstalledModule Microsoft.Graph.* | select *name*

5. Vérifiez que la liste des sous-modules installés comprend les trois sous-modules suivants utilisés dans des exercices ultérieurs du labo : 

    - Microsoft.Graph.Groups
    - Microsoft.Graph.Identity.DirectoryManagement
    - Microsoft.Graph.Users
    
    Si les trois sous-modules s’affichent dans la liste des sous-modules installés, passez à l’étape suivante. Toutefois, si l’un de ces trois sous-modules ne s’affiche pas dans la liste, exécutez la commande PowerShell suivante pour installer manuellement le sous-module manquant :

        Install-Module -Name <module name> -Scope CurrentUser

    Par exemple, si le module Microsoft.Graph.Identity.DirectoryManagement n’a pas été installé, vous exécutez la commande suivante :

        Install-Module -Name Microsoft.Graph.Identity.DirectoryManagement

6. Les paramètres de stratégie d’exécution de PowerShell imposent les scripts PowerShell qui doivent être exécutés sur un système Windows. Définir cette stratégie sur **Non approuvé** permet à Holly de charger tous les fichiers config et d’exécuter tous les scripts. À l'invite de commandes, tapez la commande suivante et appuyez sur Entrée :   <br/>

        Set-ExecutionPolicy RemoteSigned

    ‎Si vous êtes invité à confirmer que vous souhaitez modifier la stratégie d’exécution, entrez **A** pour sélectionner **[A] Oui pour tout.** 

7. Laissez votre fenêtre PowerShell ouverte, car vous l’utiliserez dans la tâche suivante.


Félicitations ! Vous avez terminé toutes les étapes pour mettre en place votre locataire de labo. Vous êtes maintenant prêt à effectuer les autres exercices de labo.

# Fin du labo 1
