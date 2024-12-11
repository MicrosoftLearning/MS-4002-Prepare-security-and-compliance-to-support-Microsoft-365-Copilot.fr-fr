# Parcours d’apprentissage 1 - Labo 2 - Exercice 2 - Gérer les rôles et les groupes de rôles

Dans cet exercice, vous allez continuer à jouer le rôle d’Holly Dickson, la nouvelle administratrice Microsoft 365 d’Adatum. Dans le cadre du projet pilote Microsoft 365 d’Adatum, vous allez gérer la délégation de l’administration en attribuant des rôles Administrateur Microsoft 365 à plusieurs des comptes d’utilisateur Microsoft 365 créés par votre fournisseur d’hébergement de labo. Cet exercice vous offrira l’opportunité d’appliquer trois méthodes différentes pour attribuer ces rôles : 1) En attribuant un rôle directement à un compte d’utilisateur dans le Centre d’administration Microsoft 365, 2) En créant un groupe de rôles, en attribuant des rôles au groupe de rôles, puis en attribuant le groupe de rôles à un utilisateur dans le Centre d’administration Microsoft 365, et 3) En attribuant un rôle à un utilisateur à l’aide de Windows PowerShell. Une fois que vous aurez attribué des rôles Administrateur Microsoft 365 à plusieurs comptes d’utilisateur existants, vous testerez ces attributions en vérifiant que les utilisateurs disposent des autorisations nécessaires pour agir conformément à leurs rôles.

### Tâche 1 - Attribuer un rôle Administrateur dans le Centre d’administration Microsoft 365

Le rôle Administrateur général Microsoft 365 a été octroyé à Holly Dickson. Continuant à jouer le rôle d’Holly, vous utiliserez le Centre d’administration Microsoft 365 pour attribuer des droits d’administrateur à l’un des utilisateurs Adatum. Durant cette tâche, vous attribuerez le rôle Administrateur de facturation au compte d’utilisateur de Diego Siciliani.

1. Dans l’exercice de labo précédent, vous avez créé un domaine pour Adatum sur LON-DC1. Vous devez maintenant revenir à **LON-CL1** pour effectuer les tâches d’administration Microsoft 365 dans cet exercice de labo. En guise de meilleure pratique, les tâches d’administration Microsoft 365 classiques doivent être effectuées sur un PC client plutôt que sur le contrôleur de domaine de l’entreprise.  <br/>

    Basculez vers **LON-CL1**. 

2. Sur **LON-CL1**, dans le **Centre d’administration Microsoft 365** dans votre navigateur Edge, vous devriez toujours être connecté en tant qu’Holly Dickson suite à un exercice de labo précédent. Dans le volet de navigation, sélectionnez **Utilisateurs**, puis **Utilisateurs actifs**. 

3. Dans la liste **Utilisateurs actifs**, sélectionnez **Diego Siciliani**.  <br/>

    **Remarque :** Sélectionnez le nom de Diego ; ne cochez pas la case à gauche de son nom. La case à cocher sert généralement à sélectionner plusieurs utilisateurs lorsque vous souhaitez effectuer l’une des actions liées à l’utilisateur dans la barre de menus qui apparaît au-dessus de la liste des utilisateurs, telles que **Gérer les licences de produit** et **Gérer les rôles**. La sélection du nom d’un utilisateur ouvre un volet de propriétés spécifiquement pour cet utilisateur.

4. Dans le volet **Diego Siciliani** qui s’affiche, l’onglet **Compte** est affiché par défaut. Sous cet onglet, faites défiler jusqu’à la section **Rôles** et sélectionnez **Gérer les rôles**. 

5. Dans la fenêtre **Gérer les rôles Administrateur**, l’option **Utilisateur (aucun accès au centre d’administration)** est actuellement sélectionnée par défaut. Maintenant que vous souhaitez attribuer un rôle Administrateur à Diego, sélectionnez l’option **Accès au centre d’administration**. Une liste de rôles Administrateur couramment utilisés s’affiche pour sélection. 

6. Diego a été promu Administrateur de facturation, mais ce rôle ne figurant pas dans la liste des rôles couramment utilisés, vous devez faire défiler vers le bas et sélectionner **Afficher tout par catégorie**. 

7. Dans la liste des rôles triés par catégorie, faites défiler vers le bas jusqu’à la catégorie **Autre**, cochez la case **Administrateur de facturation**, puis sélectionnez **Enregistrer les modifications**. <br/>

    **Conseil :** Notez le message qui s’affiche en haut du volet une fois que la modification du rôle Administrateur est enregistrée. Ce message fournit la meilleure pratique suivante que vous devez garder à l’esprit lors de la tenue à jour des rôles d’administration dans vos déploiements réels : **Accordez aux utilisateurs uniquement l’accès dont ils ont besoin en attribuant le rôle le moins permissif.**

8. Dans la fenêtre **Gérer les rôles Administrateur**, sélectionnez le **X** dans le coin supérieur droit de l’écran pour fermer la fenêtre. Vous revenez alors à la liste **Utilisateurs actifs**. 

9. Restez connecté à LON-CL1 et au Centre d’administration Microsoft 365 en tant que Holly Dickson.


### Tâche 2 : Attribuer un rôle Administrateur à l’aide d’un groupe de rôles dans le Centre d’administration Microsoft 365

Lors de la tâche précédente, vous avez attribué un rôle Administrateur directement au compte d’utilisateur de Diego Siciliani dans le Centre d’administration Microsoft 365. Durant cette tâche, vous allez attribuer des rôles au moyen d’un groupe de rôles. Vous allez créer un groupe de rôles Sécurité, lui attribuer des rôles de gestion des utilisateurs, puis attribuer ce groupe de rôles au compte d’utilisateur de Lynne Robbin dans le Centre d’administration Microsoft 365.

1. Sur LON-CL1, vous devriez toujours être connecté au Centre d’administration Microsoft 365 en tant que Holly Dickson. Si ce n’est pas le cas, établissez la connexion maintenant.

2. Dans le **Centre d’administration Microsoft 365**, sélectionnez **Équipes + groupes** dans le volet de navigation, puis **Équipes et groupes actifs**. 

3. Dans la page **Équipes et groupes actifs**, l’onglet **Groupes Teams et Microsoft 365** s’affiche par défaut. Sélectionnez l’onglet **Groupes de sécurité**.

4. Sous l’onglet **Groupes de sécurité**, sélectionnez **+Ajouter un groupe de sécurité** dans la barre de menus. Cela lance l’Assistant **Ajouter un groupe de sécurité**.

5. Dans l’Assistant **Ajouter un groupe de sécurité**, dans la page **Configurer les éléments de base**, entrez le **Groupe de rôles de gestion des utilisateurs** dans le champ **Nom**. Entrez **Ce groupe de rôles contient des rôles de gestion des utilisateurs** dans le champ **Description**. Cliquez sur **Suivant**.

6. Dans la page **Modifier les paramètres**, cochez la case **Vous pouvez assigner des rôles Azure AD au groupe**, puis sélectionnez **Suivant**.

7. Dans la page **Vérifier et terminer l’ajout d’un groupe**, passez en revue les paramètres. Si des paramètres doivent être modifiés, sélectionnez l’option **Modifier** appropriée et apportez la modification. Lorsque tous les paramètres sont corrects, sélectionnez **Créer le groupe**.

8. Une fois le **Groupe de rôles de gestion des utilisateurs** créé, sélectionnez **Fermer**.

9. Maintenant que vous avez créé le groupe de rôles, vous devez lui attribuer les rôles correspondants. Dans la page **Équipes et groupes actifs**, l’onglet **Groupes de sécurité** est affiché. Sélectionnez le **Groupe de rôles de gestion des utilisateurs** pour ouvrir son volet d’informations.

10. Dans le volet **Groupe de rôles de gestion des utilisateurs**, l’onglet **Général** est affiché par défaut. Dans la section **Rôles**, sélectionnez **Gérer les rôles**.

11. Dans le volet **Gérer les rôles Administrateur** qui s’affiche, sélectionnez l’option **Accès au Centre d’administration**. Dans la liste des rôles Administrateur courants qui s’affiche directement sous cette option, cochez les cases **Administrateur d’utilisateurs** et **Gestionnaire de réussite de l’expérience utilisateur**. Sélectionnez ensuite l’option **Tout afficher par catégorie**. Faites défiler jusqu’à la catégorie **Identité**. Notez que le rôle **Administrateur d’utilisateurs** est déjà sélectionné, car vous l’avez sélectionné précédemment dans la liste des rôles couramment utilisés. Dans cette catégorie **Identité**, sélectionnez le rôle **Administrateur de service de support**, puis sélectionnez **Enregistrer les modifications**. 

12. Dans le volet **Gérer les rôles Administrateur**, les trois rôles sélectionnés doivent apparaître sous l’option **Accès au Centre d’administration**. Cliquez sur le **X** dans le coin supérieur droit du volet pour le fermer.

13. Sous l’onglet **Groupes de sécurité**, sélectionnez **Groupe de rôles de gestion des utilisateurs**. Dans le volet **Groupe de rôles de gestion des utilisateurs** qui s’affiche, vérifiez que les trois rôles sont visibles dans la section **Rôles**. Fermez ce panneau.

14. Maintenant que vous avez attribué les rôles au groupe de rôles, vous devez attribuer le groupe de rôles au compte d’utilisateur de Lynne Robbin. Dans le **Centre d’administration Microsoft 365**, sélectionnez **Utilisateurs actifs**.

15. Dans la page **Utilisateurs actifs**, sélectionnez **Lynne Robbins**. 

16. Dans le volet **Lynne Robbins** qui s’affiche, l’onglet **Compte** est affiché par défaut. Durant la tâche précédente, lorsque vous avez attribué le rôle Administrateur de facturation au compte de Diego Siciliani, vous avez sélectionné l’option **Gérer les rôles** dans la section **Rôles**. Toutefois, étant donné que vous allez attribuer les rôles de Lynne par le biais d’un groupe de rôles, vous devez affecter Lynne en tant que membre du groupe de rôles Sécurité que vous venez de créer. C’est par le biais de l’attribution de groupe que Lynne héritera des rôles attribués au groupe de rôles. Par conséquent, dans la section **Groupes** , sélectionnez **Gérer les groupes**. 

17. Dans le volet **Gérer les groupes**, sélectionnez **+Attribuer des appartenances**.

18. Dans le volet **Attribuer des appartenances**, cochez la case **Groupe de rôles de gestion des utilisateurs**, puis sélectionnez **Ajouter(1)**.

19. Une fois qu’une notification **Enregistré** apparaît en haut de la page, fermez ce volet. 

20. Pour vérifier que Lynne a hérité des rôles qui ont été attribués au groupe de rôles de gestion des utilisateurs, sélectionnez **Lynne Robbins** dans la liste des utilisateurs actifs. 

21. Dans le volet **Lynne Robbins** qui s’affiche, sous l’onglet **Compte** affiché par défaut, vous devez voir les trois rôles de gestion des utilisateurs qui ont été attribués à Lynne. Dans la section **Rôles****, sélectionnez **Gérer les rôles**.

22. Dans le volet **Gérer les rôles Administrateur** qui s’affiche, sous l’option **Accès au Centre d’administration**, notez les trois rôles sélectionnés et le nom du groupe à partir duquel ils ont été attribués à Lynne. Notez également que les trois rôles sont grisés. Cela indique que vous ne pouvez pas les désélectionner dans cette fenêtre. Étant donné que ces rôles ont été attribués à Lynne à partir d’un groupe de rôles qui les contenait, vous ne pouvez annuler l’attribution des rôles qu’en supprimant l’appartenance de Lynne au groupe de rôles. Vous venez de vérifier que ces rôles étaient attribués à Lynne. Fermez ce volet **Gérer les rôles Administrateur**.

23. Restez connecté à LON-CL1 et au Centre d’administration Microsoft 365 en tant que Holly Dickson.

### Tâche 3 – Attribuer un rôle Administrateur à l’aide de Windows PowerShell  

Durant cette tâche, vous allez utiliser Windows PowerShell pour attribuer un rôle à un compte d’utilisateur. Cela vous offrira l’opportunité d’effectuer cette opération de gestion dans PowerShell (certains administrateurs préfèrent effectuer ce genre de maintenance à l’aide de PowerShell).

Durant cette tâche, Holly souhaite attribuer le rôle Administrateur de support de service à Patti Fernandez. Pour ajouter un utilisateur à un rôle Administrateur à l’aide du module Microsoft Graph PowerShell, vous devez d’abord obtenir l’ID d’objet de l’utilisateur et l’ID d’objet du rôle. Dans cette tâche, vous allez utiliser Microsoft Graph pour obtenir les ID respectifs, puis créer l’attribution de rôle. 

PowerShell vous permet également d’afficher tous les utilisateurs affectés à un rôle spécifique, ce qui peut être très important lors de l’audit de votre déploiement Microsoft 365. Durant cette tâche, vous allez également apprendre à utiliser PowerShell pour afficher tous les utilisateurs affectés à un rôle spécifique.

1. Sur LON-CL1, sélectionnez l’icône Windows PowerShell dans la barre des tâches que vous avez laissée ouverte suite à un labo précédent. Si vous avez fermé la fenêtre PowerShell, ouvrez une instance avec élévation de privilèges à l’aide de la même instruction que précédemment. 

2. Dans l’exercice de labo précédent, vous vous êtes connecté à Microsoft Graph et vous avez demandé des autorisations « Directory.ReadWrite.All » pour exécuter les applets de commande qui ont restauré le groupe supprimé. Pour mettre à jour les objets utilisateur et rôle dans cette tâche, Holly doit maintenant demander des autorisations de lecture/écriture pour chaque objet. Pour demander ces autorisations, tapez la commande suivante à l’invite de commandes, puis appuyez sur Entrée :  <br/>

        Connect-MgGraph -Scopes 'User.ReadWrite.All', 'RoleManagement.ReadWrite.Directory'

3. Dans la fenêtre **Choisir un compte** qui s’affiche, sélectionnez le compte d’Holly Dickson.

4. Dans la boîte de dialogue **Autorisations demandées** qui s’affiche, cochez la case **Consentement pour le compte de votre organisation**, puis sélectionnez **Accepter**.

5. Holly souhaite affecter **Patti Fernandez** au rôle **Administrateur de support de service**. Pour attribuer ce rôle à l’aide de Microsoft Graph PowerShell, vous devez d’abord obtenir l’ID d’objet du rôle Administrateur de support de service afin de pouvoir l’affecter à Patti.

    **Important :** Avant d’effectuer cette étape, vérifiez que votre fenêtre PowerShell est en mode plein écran. Le nom du rôle apparaît dans la deuxième colonne de la sortie. Si vous n’êtes pas en mode plein écran, vous ne verrez pas le nom du rôle associé à chaque ID d’objet. 

6. Pour attribuer un rôle dans Microsoft Graph PowerShell, vous devez d’abord localiser son ID d’objet. Il existe deux manières d’afficher les modèles de rôle : vous pouvez soit afficher l’intégralité de la liste des modèles de rôle, soit afficher le modèle pour un rôle spécifique. En guise d’expérience d’apprentissage, vous appliquerez les deux méthodes afin de voir la différence. <br/>

    Commençons par afficher la liste complète des modèles de rôle, ainsi que leur ID d’objet et leur nom d’affichage. Pour ce faire, tapez la commande suivante, puis appuyez sur Entrée : <br/>

        Get-MgDirectoryRoleTemplate | Sort DisplayName | Format-Table Id, DisplayName

    Comme vous pouvez le voir après avoir exécuté cette commande, vous devez parcourir la liste des modèles de rôle à la recherche du rôle Administrateur de support de service. Vous pouvez aisément constater à quel point cela peut être fastidieux, même en triant le tableau. En guise d’alternative, exécutez la commande suivante pour rechercher un modèle de rôle spécifique, en l’occurrence le modèle de rôle « Administrateur de support de service » : <br/>

        Get-MgDirectoryRoleTemplate | ? DisplayName -eq "Service Support Administrator" | Format-Table Id, DisplayName

    Une fois cette commande exécutée, vous pouvez constater qu’elle affiche uniquement le modèle de rôle demandé. Évidemment, il peut arriver que l’affichage de la liste complète des modèles de rôle soit nécessaire. Toutefois, lorsque vous devez rechercher un modèle de rôle unique, il sera beaucoup plus efficace d’exécuter la deuxième commande PowerShell que d’avoir à parcourir la liste complète des modèles.

7. Pour affecter Patti Fernandez au rôle Administrateur de support de service que vous venez d’activer, vous devez d’abord obtenir l’ID d’objet du compte d’utilisateur de Patti. Pour cela, tapez la commande suivante et appuyez sur Entrée :

        Get-MgUser -Filter "DisplayName eq 'Patti Fernandez'" | Format-Table ID, DisplayName

8. Maintenant que vous connaissez l’ID d’objet du rôle Administrateur de support de service et l’ID d’objet du compte d’utilisateur de Patti, vous pouvez attribuer le rôle à Patti. Suivez les étapes ci-après pour effectuer ce processus, en remplaçant les deux ID par les valeurs affichées dans les deux étapes précédentes.

        New-MgRoleManagementDirectoryRoleAssignment -RoleDefinitionId 'paste in the role ID here' -PrincipalId 'paste in Pattis ID here' -DirectoryScopeId '/'

    **Note :** le paramètre DirectoryScopeId indique que l’attribution est effectuée au niveau du locataire/du répertoire.

9. Vous souhaitez maintenant vérifier que Patti a été affectée au rôle Administrateur de support de service. Pour ce faire, nous allons exécuter deux commandes. La première obtient le rôle attribué et le stocke dans une variable, et la seconde affiche les ID des utilisateurs affectés au rôle.

        $assignedRole = Get-MgDirectoryRole -Filter "DisplayName eq 'Service Support Administrator'"
        Get-MgDirectoryRoleMember -DirectoryRoleId $assignedRole.Id

10. La commande précédente affiche uniquement les ID des utilisateurs affectés au rôle sélectionné. Toutefois, vous pouvez mettre en correspondance l’ID affiché avec l’ID de Patti afin de vérifier que son compte a été affecté au rôle **Administrateur de support de service**. Comme vous pouvez le constater, Patti est la seule utilisatrice affectée au rôle. 

11. Répétons maintenant ce processus pour voir tous les utilisateurs affectés au rôle Administrateur général.

        $assignedRole = Get-MgDirectoryRole -Filter "DisplayName eq 'Global Administrator'"
        Get-MgDirectoryRoleMember -DirectoryRoleId $assignedRole.Id

12. Vérifiez que le rôle Administrateur général a été attribué à plusieurs utilisateurs Adatum. Dans un scénario réel, l’administrateur Microsoft 365 utiliserait cette commande PowerShell afin de surveiller le nombre d’administrateurs généraux présents dans son déploiement Microsoft 365. Il supprimerait ensuite le rôle Administrateur général de tous les utilisateurs qui n’ont aucune bonne raison de le détenir (n’oubliez pas que les recommandations en matière de meilleures pratiques consistent à avoir entre deux et quatre administrateurs généraux dans un déploiement Microsoft 365, en fonction de la taille de l’organisation).  <br/>

    Dans le cas de ce labo, votre fournisseur d’hébergement de labo a attribué le rôle Administrateur général à des utilisateurs autres que l’Administrateur MOD (et vous l’avez attribué à Holly Dickson), et vous laisserez ces utilisateurs tels quels. Dans ce déploiement fictif d’Adatum, il n’y a aucun intérêt à ce que vous perdiez votre temps à supprimer ce rôle de leurs comptes. De plus, certaines tâches ultérieures de labo impliquent l’attribution du rôle Administrateur général à ces utilisateurs. <br/>

    **IMPORTANT :** N’oubliez pas que dans votre déploiement réel, l’Administrateur Microsoft 365 doit surveiller régulièrement le rôle Administrateur général afin que le nombre d’utilisateurs attribués reste compris entre deux et quatre.
    
13. Laissez votre session Windows PowerShell ouverte pour les exercices ultérieurs de labo, mais réduisez-la avant de passer à la tâche suivante.


### Tâche 4 – Valider les attributions de rôles 

Durant cette tâche, vous allez commencer par examiner les propriétés administratives de deux utilisateurs, Joni Sherman et Lynne Robbins. Ensuite, vous vous connecterez à la page d’accueil de Microsoft 365 sur la machine virtuelle Client 2 (LON-CL2) sous le compte de chaque utilisateur afin de confirmer plusieurs des modifications que vous avez apportées lors de la gestion de leur délégation administrative durant les tâches précédentes. Pour finir, en tant que Lynne Robbins, vous effectuerez deux tâches importantes de maintenance de compte d’utilisateur : la réinitialisation de mots de passe et le blocage de comptes d’utilisateur.

1. Sur LON-CL1, vous devriez toujours être connecté au Centre d’administration Microsoft 365 en tant que Holly Dickson. Si ce n’est pas le cas, établissez la connexion maintenant.

2. Dans le **Centre d’administration Microsoft 365**, si vous n’êtes pas dans la page **Utilisateurs actifs**, accédez-y maintenant.  

3. Dans la liste **Utilisateurs actifs**, sélectionnez **Joni Sherman**. 

4. Dans la fenêtre des propriétés de **Joni Sherman**, l’onglet **Compte** est affiché par défaut. Dans la section **Rôles**, il doit être indiqué que Joni n’a **Pas d’accès administrateur**. Sélectionnez le **X** dans le coin supérieur droit pour fermer la fenêtre de propriétés de Joni.

5. Dans la liste **Utilisateurs actifs**, sélectionnez **Lynne Robbins**. 

6. Dans la fenêtre de propriétés de ** Lynne Robbins**, il doit être indiqué que Lynne a été affectée au rôle **Administrateur d’utilisateurs**. Fermez la fenêtre de propriétés de Lynne.

7. Basculez vers la machine virtuelle Client 2 (**LON-CL2**).

8. Dans **LON-CL2**, sur l’écran de connexion, vous allez vous connecter en tant que compte **LON-CL2\Admin** local avec le mot de passe **Pa55w.rd**.

9. Si une fenêtre **Réseaux** s’affiche, sélectionnez **Oui**.

10. Dans la barre des tâches, sélectionnez l’icône **Microsoft Edge**. Agrandissez votre fenêtre de navigateur Edge si nécessaire.

11. Dans votre navigateur **Edge**, accédez à **https://portal.office.com**. 

12. Vous commencerez par vous connecter à Microsoft 365 en tant que **Joni Sherman**. Dans la fenêtre **Se connecter**, entrez **JoniS@xxxxxZZZZZZ.onmicrosoft.com** (où xxxxxZZZZZZ est le préfixe de locataire fourni par votre fournisseur d’hébergement de labo). Étant donné que vous vous connectez en tant que Joni Sherman, entrez ce **Mot de passe de l'utilisateur** fourni par votre fournisseur d’hébergement de laboratoire dans la fenêtre **Entrer le mot de passe**. <br>

    Dans la boîte de dialogue **Mettre à jour votre mot de passe** qui s’affiche, entrez le **Mot de passe de l'utilisateur** fourni par votre fournisseur d’hébergement de labo dans le champ **Mot de passe actuel**. Entrez ensuite le nouveau Mot de passe utilisateur dans les champs **Nouveau mot de passe** et **Confirmer le mot de passe**, puis sélectionnez **Se connecter**.

13. Dans la fenêtre **Rester connecté ?**, cochez la case **Ne plus afficher**, puis sélectionnez **Oui**. Si une fenêtre **Enregistrer le mot de passe** s’affiche, sélectionnez **Jamais**.

14. Si une boîte de dialogue **Bienvenue dans Microsoft 365** s’affiche au milieu de la page, sélectionnez deux fois la flèche vers l’avant (>), puis la coche pour fermer la boîte de dialogue.

15. Si une fenêtre **Rechercher d’autres applications** ou une fenêtre **Créer avec Microsoft 365** ou toute autre fenêtre de type introduction s’affiche, sélectionnez le **X** dans le coin supérieur de la fenêtre pour la fermer.

16. Dans la fenêtre **Bienvenue dans Microsoft 365**, qui est la page d’accueil Microsoft 365 de Joni, un volet de navigation sur le côté de l’écran indique les applications auxquelles l’utilisateur est autorisé à accéder. Dans ce volet **Applications**, notez que l’option **Administrateur** n’est pas affichée. Cela est dû au fait que Joni n’a jamais été affecté à un rôle Administrateur Microsoft 365. 

17. Vous allez maintenant vous déconnecter de Microsoft 365 en tant que Joni. Dans **Microsoft Edge**, en haut à droite de la page **Bienvenue dans Microsoft 365**, sélectionnez l’icône d’utilisateur pour **Joni Sherman** (le cercle dans le coin supérieur avec la photo de Joni), et dans la fenêtre **Joni Sherman** qui s’affiche, sélectionnez **Se déconnecter**. 

18. Vous allez maintenant vous reconnecter à Microsoft 365 en tant que **Lynne Robbins**. Votre onglet de navigateur **Edge** actif doit afficher un message indiquant **Joni, vous êtes maintenant déconnecté(e)**. Dans cette fenêtre, vous avez le choix entre vous reconnecter en tant que Joni ou vous connecter en tant qu’un autre utilisateur. <br/>

    Sélectionnez **Basculer vers un autre compte** puis, dans le champ **Adresse e-mail** qui s’affiche, entrez ****LynneR@xxxxxZZZZZZ.onmicrosoft.com (où xxxxxZZZZZZ est le préfixe de locataire fourni par votre fournisseur d’hébergement de labo), puis sélectionnez **Se connecter**. Dans la fenêtre **Entrer un mot de passe**, entrez le **mot de passe utilisateur** fourni par votre fournisseur d’hébergement de labo, puis sélectionnez **Se connecter**. <br>

    Dans la boîte de dialogue **Mettre à jour votre mot de passe** qui s’affiche, entrez le **Mot de passe de l'utilisateur** fourni par votre fournisseur d’hébergement de labo dans le champ **Mot de passe actuel**. Entrez ensuite le nouveau Mot de passe utilisateur dans les champs **Nouveau mot de passe** et **Confirmer le mot de passe**, puis sélectionnez **Se connecter**. 

19. Si une boîte de dialogue **Bienvenue dans Microsoft 365** s’affiche, sélectionnez deux fois la flèche vers l’avant (>), puis cochez la case pour fermer la fenêtre.

20. Si une fenêtre **Rechercher d’autres applications** ou une fenêtre **Créer avec Microsoft 365** ou toute autre fenêtre de type introduction s’affiche, sélectionnez le **X** dans le coin supérieur de la fenêtre pour la fermer.

21. Dans la fenêtre **Bienvenue dans Microsoft 365**, qui est la page d’accueil Microsoft 365 de Lynne, notez que l’icône **Administrateur** est visible dans le volet de navigation sur le côté de l’écran. Cela est dû au fait que Lynne a été affectée à un rôle Administrateur Microsoft 365. Sélectionnez l’icône **Administrateur** pour ouvrir le Centre d’administration Microsoft 365.

22. Dans le **Centre d’administration Microsoft 365**, sélectionnez **Utilisateurs** dans le volet de navigation, puis **Utilisateurs actifs**. 

23. En tant qu’**Administrateur d’utilisateurs**, Lynne a l’autorisation de modifier les mots de passe des utilisateurs. Lynne a récemment été contactée par **Diego Siciliani** et **Pradeep Gupta**, qui ont chacun signalé que leurs mots de passe avaient peut-être été compromis. Conformément à la stratégie d’entreprise de Per Adatum, Lynne doit réinitialiser leurs mots de passe à une valeur temporaire, puis les forcer à réinitialiser leur mot de passe lors de leur prochaine connexion.   <br/>

    Dans la liste **Utilisateurs actifs**, lorsque vous déplacez votre souris d’un compte d’utilisateur vers un autre, notez l’icône de **clé (Réinitialiser un mot de passe)** qui apparaît à droite du nom de chaque utilisateur. Sélectionnez l’icône de clé qui apparaît à droite du nom de **Diego Siciliani**.

24. Dans la fenêtre **Réinitialiser le mot de passe** pour Diego, si la case ** Créer automatiquement un mot de passe** est cochée, décochez-la. Cela permettra à Lynne d’attribuer manuellement un mot de passe temporaire à Diego.  

25. Entrez **diego** dans le champ **Mot de passe**. Notez qu’à droite du mot de passe, le système affiche un message indiquant qu’il s’agit d’un mot de passe **faible**. Notez également le message qui apparaît sous le champ, indiquant les conditions requises pour un mot de passe fort. Pour finir, notez que le bouton **Réinitialiser le mot de passe** en bas du volet n’est pas activé. **Ce bouton ne sera activé qu’une fois que vous aurez entré un mot de passe fort**.  

26. Vérifiez que la case **Demander à cet utilisateur de modifier son mot de passe lors de sa première connexion** est cochée (si ce n’est pas le cas, cochez-la). Entrez **Pa55w.rd** dans le champ **Mot de passe**. Notez que le champ **Mot de passe** indique qu’il s’agit d’un mot de passe fort. <br/>

    Décochez maintenant la case **Demander à cet utilisateur de modifier son mot de passe lors de sa première connexion**. Notez le message d’erreur qui s’affiche, indiquant que le mot de passe (Pa55w.rd) contient un mot, une expression ou une série de nombres qui le rend facilement détectable. En l’occurrence, vous avez entré une variante du mot **password**, ce qui déclenchera cette erreur. Le système vous autorise à entrer ce mot de passe si vous forcez l’utilisateur à le modifier lors de sa première connexion. En revanche, si vous ne forcez pas l’utilisateur à entrer un autre mot de passe lors de sa première connexion, ce mot de passe n’est pas autorisé.

27. Après ces deux tentatives de mot de passe ayant échoué, Lynne a décidé de laisser Microsoft 365 générer automatiquement un mot de passe. Cochez la case **Créer automatiquement un mot de passe**. 
    
28. Le mot de passe généré automatiquement sera uniquement un mot de passe temporaire, car Lynne souhaite forcer Diego à le modifier la prochaine fois qu’il se connectera. Par conséquent, vérifiez que la case **Demander à cet utilisateur de modifier son mot de passe lors de sa première connexion** est cochée ; si ce n’est pas le cas, cochez-la.

29. Sélectionnez **Réinitialiser le mot de passe**.

30. Si vous êtes invité à enregistrer le mot de passe, sélectionnez **jamais** pour fermer la fenêtre.

31. Vous devriez recevoir un message d’erreur indiquant que vous ne pouvez pas réinitialiser le mot de passe de Diego, car un rôle Administrateur lui a été attribué. Dans le cas de Diego, vous lui avez attribué le rôle Administrateur de facturation plus tôt dans cet exercice de labo. Étant donné que seuls les Administrateurs généraux peuvent modifier le mot de passe d’un autre administrateur et que Lynne n’est pas Administrateur général, elle devra demander à Holly Dickson d’apporter cette modification. Sélectionnez **Fermer** dans le volet **Réinitialiser le mot de passe**. 

32. Si une fenêtre de demande d’enquête s’affiche, sélectionnez **Annuler**.

33. Maintenant, modifiez le mot de passe de Pradeep Gupta. Dans la liste **Utilisateurs actifs**, sélectionnez l’icône de **clé (Réinitialiser un mot de passe)** qui s’affiche à droite de **Pradeep Gupta**. 

34. Dans la fenêtre **Réinitialiser le mot de passe** qui s’affiche pour Pradeep, vérifiez que la case **Créer automatiquement un mot de passe** est cochée ; si ce n’est pas le cas, cochez-la maintenant afin que le système génère automatiquement un mot de passe pour Pradeep.  <br/>

    Il s’agit seulement d’un mot de passe temporaire, car Lynne souhaite forcer Pradeep à le modifier la prochaine fois qu’il se connectera. Par conséquent, vérifiez que la case **Demander à cet utilisateur de modifier son mot de passe lors de sa première connexion** est cochée ; si ce n’est pas le cas, cochez-la.
    
35. Sélectionnez le bouton **Réinitialiser le mot de passe**.

36. Dans la fenêtre **Le mot de passe a été réinitialisé**, vous devez recevoir un message indiquant que vous avez réinitialisé le mot de passe de Pradeep. Sélectionnez **Fermer**.

37. La direction a récemment découvert que le nom d’utilisateur d’Alex Wilber avait peut-être été compromis. Lynne a par conséquent été chargée de bloquer le compte d’Alex afin que personne ne puisse se connecter avec son nom d’utilisateur jusqu’à ce que la direction ait pu déterminer l’étendue du problème. Dans la liste **Utilisateurs actifs**, cochez la case à gauche du nom d’**Alex Wilber** (ne sélectionnez PAS le nom d’Alex proprement dit).  <br/>

    **Important :** Étant donné que vous allez exécuter une commande globale plutôt qu’une commande associée au compte d’Alex, il faut que seul le compte d’Alex soit sélectionné dans la liste des utilisateurs actifs. Si un autre compte d’utilisateur est sélectionné, vous devez le désélectionner avant de continuer. Faites défiler la liste des utilisateurs actifs et vérifiez qu’aucun autre compte d’utilisateur n’est sélectionné. Si un compte autre que celui d’Alex est sélectionné, décochez la case correspondant à ce compte. **Seul le compte d’Alex Wilber doit être sélectionné.**

38. Dans la barre de menus en haut de la page, sélectionnez l’**icône de sélection (...)** pour afficher un menu déroulant d’actions supplémentaires. Dans le menu qui s’affiche, sélectionnez **Modifier l’état de la connexion**.

39. Dans le volet **Bloquer la connexion** qui s’affiche, vérifiez que l’adresse e-mail d’Alex apparaît sous le titre **Bloquer la connexion**. Cochez la case **Empêcher cet utilisateur de se connecter**, puis sélectionnez **Enregistrer les modifications.** 

40. La fenêtre **Bloquer la connexion** doit afficher un message indiquant qu’Alex ne peut désormais plus se connecter (et personne ne peut se connecter avec le nom d’utilisateur d’Alex si son nom d’utilisateur a réellement été compromis). En outre, Alex sera automatiquement déconnecté des services Microsoft dans les 60 minutes qui suivent. Sélectionnez le **X** dans le coin supérieur du volet pour le fermer. 

41. Lynne vient d’être informée que le nom d’utilisateur de **Nestor Wilke** avait peut-être également été compromis. Répétez les étapes 37 à 40 pour empêcher Nestor de se connecter (et pour empêcher toute autre personne d’utiliser son nom d’utilisateur pour se connecter). <br/>

    Lorsque vous avez essayé d’empêcher Nestor de se connecter, vous devez avoir reçu un message d’erreur indiquant **Impossible d’enregistrer les modifications**. La raison pour laquelle vous avez reçu cette erreur est que Nestor est un Administrateur général, contrairement à Lynne. Seul un Administrateur général peut empêcher un autre Administrateur général de se connecter. Lynne devra demander à Holly Dickson d’apporter cette modification. <br/>

    Fermez le volet **Bloquer la connexion**.

42. Vous avez précédemment fait en sorte qu’Alex Wilber ne puisse plus se connecter. Pour vérifier que le blocage est bien en vigueur, vous allez tenter de vous connecter en tant qu’Alex. Déconnectez-vous de Microsoft 365 en sélectionnant l’icône d’utilisateur pour **Lynne Robbins** (le cercle contenant l’image de Lynne dans le coin supérieur) et, dans la fenêtre **Lynne Robbins** qui s’affiche, sélectionnez **Se déconnecter**. 

43. En guise de meilleure pratique, fermez tous vos onglets de navigateur sauf **Se déconnecter** une fois que vous êtes déconnecté. Sous l’onglet **Se déconnecter**, accédez à **https://portal.office.com**. 

44. Dans la fenêtre **Choisir un compte**, sélectionnez **Utiliser un autre compte**. Dans la fenêtre **Se connecter**, entrez **AlexW@xxxxxZZZZZZ.onmicrosoft.com** (où xxxxxZZZZZZ est le préfixe de locataire fourni par votre fournisseur d’hébergement de labo). Dans la fenêtre **Entrer le mot de passe**, entrez le **mot de passe utilisateur** fourni par votre fournisseur d’hébergement de labo.  <br/>

    La fenêtre **Choisir un compte** doit apparaître et afficher un message d’erreur indiquant que **Votre compte a été verrouillé. Contactez votre support technique pour le déverrouiller, puis réessayez.** Vous venez de vérifier qu’Alex (ou quelqu’un ayant obtenu le nom d’utilisateur et le mot de passe d’Alex) ne pouvait pas se connecter. <br/>

    **Remarque :** L’implémentation complète du blocage de compte peut prendre quelques minutes. Tant que le blocage n’a pas été implémenté dans le système, il est possible qu’Alex puisse encore se connecter, mais aucun des services Microsoft 365 ne lui sera accessible, et ces services n’apparaîtront pas dans le portail Microsoft 365. Une fois qu’un compte est débloqué, les services redeviennent disponibles. <br/>

    Si vous pouvez vous connecter en tant qu’Alex, déconnectez-vous et attendez quelques minutes. Cela peut être un bon moment pour faire une petite pause. Ensuite, essayez de vous reconnecter en tant qu’Alex. À ce stade, vous devriez recevoir le message d’erreur indiquant que le compte d’Alex a été bloqué et que la connexion est impossible. 
    
45. Revenez à **LON-CL1**. 

46. Dans **LON-CL1**, vous devriez toujours être connecté à **Microsoft 365** en tant que Holly Dickson dans votre navigateur Edge. La liste **Utilisateurs actifs** doit encore être affichée dans le **Centre d’administration Microsoft 365**. 

47. Suite à une investigation approfondie, le Directeur technique d’Adatum a déterminé que le compte d’Alex Wilber n’avait en fait pas été compromis ; il a donc demandé à Holly de supprimer le blocage du compte d’utilisateur d’Alex. Répétez les étapes 37 à 40 pour débloquer son compte. Notez que la fenêtre **Bloquer la connexion** de l’étape 39 affiche désormais **Débloquer la connexion**.  <br/>

    Dans la fenêtre **Débloquer la connexion**, la case **Empêcher cet utilisateur de se connecter** est actuellement cochée. Décochez cette case, puis sélectionnez **Enregistrer les modifications**. <br/>
    
    **IMPORTANT :** Un message d’avertissement s’affiche, indiquant qu’il faudra peut-être qu’Alex patiente jusqu’à 15 minutes avant de pouvoir se reconnecter. Étant donné les contraintes de temps liées à la formation, vous n’essaierez **PAS** de vérifier si Alex peut se reconnecter. Si vous le souhaitez, vous pouvez essayer de vous connecter en tant qu’Alex ultérieurement si vous êtes en pause ou si vous avez du temps libre et que vous souhaitez tester cela. Pour l’instant, restez sur LON-CL1 et fermez simplement la fenêtre **Débloquer la connexion**.
    
48. Sur LON-CL1, laissez votre navigateur et tous les onglets ouverts, et passez à l’exercice suivant.
    

# Fin du labo 2

