# Parcours d’apprentissage 1 - Labo 2 - Exercice 1 - Gérer l’accès utilisateur sécurisé 

Les organisations doivent s’assurer que l’accès à leurs données d’entreprise sur Microsoft 365 est toujours sécurisé. Microsoft 365 affiche souvent des données sensibles et confidentielles, notamment des e-mails, des documents, des informations client et de la propriété intellectuelle. L’accès non autorisé à Microsoft 365 peut engendrer des violations de données, une usurpation d’identité et d’autres activités malveillantes. En sécurisant l’accès utilisateur, les organisations peuvent empêcher les personnes non autorisées d’accéder aux données de l’entreprise, et potentiellement d’en faire mauvais usage ou de les divulguer, lorsqu’elles utilisent Microsoft 365.

Dans l’exercice de labo suivant, vous allez continuer à jouer le rôle d’Holly Dickson, la nouvelle administratrice Microsoft 365 d’Adatum. Vous allez utiliser plusieurs fonctions de gestion des utilisateurs et des groupes dans Microsoft 365. Vous commencerez par créer un compte d’utilisateur Microsoft 365 pour Holly, à qui sera attribué le rôle Administrateur général Microsoft 365. Vous allez créer plusieurs groupes Microsoft 365 et affecter des utilisateurs Microsoft 365 existants en tant que membres de ces groupes. Vous allez ensuite supprimer l’un des groupes, puis utiliser Windows PowerShell pour récupérer le groupe supprimé.

**Remarque :** L’environnement de machine virtuelle fourni par votre fournisseur d’hébergement de labo comporte plus de 20 comptes d’utilisateur Microsoft 365, ainsi qu’un grand nombre de comptes d’utilisateur locaux. Plusieurs des comptes d’utilisateur Microsoft 365 existants seront utilisés dans les labos de ce cours. Bien que le compte Administrateur MOD ait été créé par votre fournisseur d’hébergement de labo, vous allez tout de même créer le compte d’utilisateur d’Holly Dickson, car l’attribution du rôle Administrateur général Microsoft 365 à plusieurs utilisateurs est une pratique recommandée. Cela vous offrira également l’opportunité de créer un compte d’utilisateur Microsoft 365, si vous n’êtes pas familiarisé avec le processus.

Holly a été chargée par le Directeur technique d’Adatum de déployer l’authentification multifacteur (MFA) Microsoft Entra et le verrouillage intelligent de Microsoft Entra. Ces fonctionnalités aideront à renforcer la gestion des mots de passe au sein de l’organisation en vue de l’adoption de Copilot pour Microsoft 365. Quant au verrouillage intelligent, vous le déploierez à l’aide de Gestion des stratégies de groupe. 


### Tâche 1 – Créer un compte d’utilisateur pour l’Administrateur Microsoft 365 d’Adatum

Holly Dickson est la nouvelle administratrice Microsoft 365 d’Adatum. Aucun compte d’utilisateur Microsoft 365 n’ayant été configuré pour elle, elle s’est initialement connectée à Microsoft 365 sous le compte de l’Administrateur MOD (l’Administrateur général par défaut) dans le labo précédent. Durant cette tâche, vous continuerez à être connecté en tant qu’Administrateur MOD, et créerez un compte d’utilisateur Microsoft 365 pour Holly. Vous attribuerez également le rôle Administrateur général Microsoft 365 au compte d’Holly. Ce rôle fournira à Holly les autorisations nécessaires pour effectuer toutes les fonctions administratives dans Microsoft 365. Après cette tâche, vous vous connecterez à l’aide du nouveau compte de Holly et effectuerez tous les labos restants sous ce compte. 

**Note relative aux licences :** Avant de créer le compte de Holly, vous devez d’abord vérifier le nombre de licences disponibles. Ce faisant, vous remarquerez que bien que votre locataire de labo fournisse 20 licences Microsoft 365 E5 (pas Teams) et 20 licences Microsoft Teams Enterprise, toutes ces licences ont déjà été affectées aux comptes d’utilisateur existants créés par votre fournisseur d’hébergement de labo. Par conséquent, vous devez d’abord annuler l’affectation d’une licence de chaque type d’un utilisateur existant afin de pouvoir les affecter à Holly.

**Important :** En guise de meilleure pratique dans votre déploiement réel, vous devez toujours noter les informations d’identification du premier compte d’Administrateur général (dans ce labo, il s’agit du compte Administrateur MOD, dont le nom d’utilisateur est admin@xxxxxZZZZZZ.onmicrosoft.com, où xxxxxZZZZZZ est le préfixe de locataire attribué par votre fournisseur d’hébergement de labo). Vous devez conserver ces informations de compte en lieu sûr pour des raisons de sécurité. **Ce compte doit être une identité NON personnalisée** qui détient les privilèges les plus élevés possibles dans un locataire. Il ne doit **pas** être activé pour MFA, car il n’est pas personnalisé. Le nom d’utilisateur et le mot de passe de ce premier compte d’Administrateur général étant couramment partagés entre plusieurs utilisateurs, ce compte est une cible idéale pour les attaques. Par conséquent, il est toujours recommandé aux organisations de créer des comptes d’administrateur de service personnalisés (par exemple, un administrateur Exchange, un administrateur SharePoint, et ainsi de suite) et de limiter au plus le nombre d’Administrateurs généraux personnels. Les Administrateurs généraux personnels que vous créez dans votre déploiement réel doivent chacun être mappés à un utilisateur unique (par exemple, Holly Dickson), et l’authentification multifacteur (MFA) Microsoft Entra doit être appliquée pour chacun d’eux.  

1. Sur la machine virtuelle **LON-CL1**, le **Centre d’administration Microsoft 365** doit toujours être ouvert dans votre navigateur Microsoft Edge suite à l’exercice de labo précédent. Vous devez être connecté à Microsoft 365 en tant qu’**Administrateur MOD**. 

2. Étant donné que vous ajoutez un nouvel utilisateur, vous devez commencer par vérifier la disponibilité des licences avant d’ajouter le compte d’utilisateur. Dans le volet de navigation du **Centre d’administration Microsoft 365**, sélectionnez **Facturation** pour développer le groupe Facturation, puis sélectionnez **Licences**. 

3. Dans la page **Licences**, l’onglet **Abonnements** est affiché par défaut. Dans la liste des abonnements, notez que les abonnements **Microsoft 365 E5 (pas Teams)** et **Microsoft Teams Enterprise** n’ont pas de licences disponibles. Votre locataire de labo fournit 20 licences pour chaque abonnement, mais les 40 licences ont été attribuées. Étant donné que vous devez affecter à Holly à la fois une licence **Microsoft 365 E5 (pas Teams)** et une licence **Microsoft Teams Enterprise**, vous devez d’abord annuler l’affectation des licences d’un compte d’utilisateur existant afin de les mettre à disposition d’Holly. 

4. Dans le volet de navigation du **Centre d’administration Microsoft 365**, sélectionnez **Utilisateurs**, puis **Utilisateurs actifs**. Dans la liste **Utilisateurs actifs**, vous verrez la liste des comptes d’utilisateur existants qui ont été créés par votre fournisseur d’hébergement de labo. Étant donné que Christie Cline assumera un nouveau rôle au sein de l’entreprise et ne fera plus partie du projet pilote Microsoft 365, vous allez annuler l’attribution des licences **Microsoft 365 E5 (pas Teams)** et **Microsoft Teams Enterprise** à partir de son compte, afin de pouvoir les réaffecter au nouveau compte d’Holly Dickson.

5. Dans la page **Utilisateurs actifs**, dans la liste des utilisateurs, sélectionnez **Christie Cline** (sélectionnez le nom de Christie en lien hypertexte, et non la case à cocher en regard de son nom).

6. Dans le volet **Christie Cline** qui s’affiche, l’onglet **Compte** s’affiche par défaut. Sélectionnez l’onglet **Licences et applications**. Sous **Licences (2)**, cochez les cases à côté de **Microsoft 365 E5 (pas Teams)** et **Microsoft Teams Enterprise** pour les effacer, puis sélectionnez **Enregistrer les modifications**. Une fois les modifications enregistrées, fermez le volet **Christie Cline**. 

7. Vous êtes maintenant prêt à créer un compte d’utilisateur pour Holly Dickson, la nouvelle administratrice Microsoft 365 d’Adatum. Vous attribuerez à Holly le rôle Administrateur général Microsoft 365, qui lui donnera un accès global à la plupart des fonctionnalités de gestion et des données dans les services en ligne Microsoft. Vous affecterez également à Holly les deux licences que vous venez de retirer de Christie Cline. <br/>

    Dans la fenêtre **Utilisateurs actifs**, sélectionnez l’option **Ajouter un utilisateur** qui apparaît dans la barre de menus au-dessus de la liste des utilisateurs actifs. Cela démarre l’assistant **Ajouter un utilisateur**.

8. Dans la page **Configurer les éléments de base** de l’Assistant **Ajouter un utilisateur**, entrez les informations suivantes :

    - Prénom : **Holly**

    - Nom : **Dickson** 

    - Nom complet : Lorsque vous accédez à cet onglet dans ce champ, **Holly Dickson** s’affiche.

    - Nom d’utilisateur : **Holly** <br/>
    
        ‎**IMPORTANT :** À droite du champ **Nom d’utilisateur** figure le champ de domaine. Il est prérenseigné avec le domaine **xxxxxZZZZZZ.onmicrosoft.com** (où xxxxxZZZZZZ est le préfixe de locataire fourni par votre fournisseur d’hébergement de labo).<br/>
    
    - Décochez la case **Créer automatiquement un mot de passe**, ce qui affichera un nouveau champ pour entrer un mot de passe défini par l’administrateur.

    - Saisissez le nouveau mot de passe d’administration dans le champ **Mot de passe** qui s’affiche (il s’agit du **nouveau mot de passe d’administration** que vous avez été invité à créer au début du labo 1, exercice 1).

    - Décochez la case **Demander à cet utilisateur de modifier son mot de passe lors de sa première connexion**. 

9. Cliquez sur **Suivant**. Si une boîte de dialogue **Enregistrer le mot de passe** s’affiche en haut de l’écran, sélectionnez **Jamais**.

10. Dans la page **Affecter des licences de produits**, entrez les informations suivantes : <br/>

    - Sélectionnez l’emplacement : **États-Unis**

    - Licences : Sous l’option **Affecter une licence de produit à l’utilisateur**, cochez les cases **Microsoft 365 E5 (pas Teams)** et **Microsoft Teams Enterprise**

11. Cliquez sur **Suivant**.

12. Dans la page **Paramètres facultatifs** , sélectionnez la flèche déroulante à droite de **Rôles**. 

13. Dans la section **Rôles**, sélectionnez l’option **Accès au Centre d’administration** . Lorsque vous sélectionnez cette option, les rôles d’administrateur Microsoft 365 aux niveaux inférieurs les plus couramment utilisés sont activés.  <br/>

    **Remarque :** Tous les rôles d’administrateur s’affichent si vous sélectionnez **Tout afficher par catégorie**, qui apparaît après le dernier rôle courant. Pour Holly, vous n’avez pas besoin d’afficher tous les rôles d’administrateur par catégorie, car elle recevra le rôle Administrateur général qui figure dans la liste des rôles couramment utilisés.

14. Cochez la case **Administrateur général**. <br/>

    **Remarque :** Un message d’avertissement s’affiche, indiquant qu’Adatum a déjà sept Administrateurs généraux. Dans un environnement normal, cela serait excessif et non recommandé. Pour les besoins de ce labo, le fournisseur d’hébergement de labo a attribué le rôle Administrateur général à l’Administrateur MOD et six autres comptes d’utilisateur, ce qui n’est pas quelque chose que vous verriez normalement dans un déploiement réel. Toutefois, dans le cadre de ce labo dans votre environnement de labo Adatum fictif, vous pouvez ignorer ce message. **Ceci étant dit, la meilleure pratique que vous devez suivre consiste à avoir de deux à quatre Administrateurs généraux dans vos déploiements Microsoft 365 réels.** 

15. Cliquez sur **Suivant**.

16. Dans la fenêtre **Vérifier, puis terminer**, passez en revue vos sélections. Si quelque chose doit être modifié, sélectionnez le lien **Modifier**approprié et apportez les modifications nécessaires. Autrement, si tout est correct, sélectionnez **Terminer l’ajout**. 

17. Sur la page **Holly Dickson a été ajoutée aux utilisateurs actifs**, dans la section **Détails de l’utilisateur**, sélectionnez l’option **Afficher** pour vérifier que le mot de passe d’Holly est le même **mot de passe d’administration** que celui que vous avez été invité à créer au début du labo 1, exercice 1.  <br/>

    **Remarque :** Si vous avez entré accidentellement un autre mot de passe, une fois revenu à la page **Utilisateurs actifs**, vous devrez sélectionner l’icône **Réinitialiser un mot de passe** (l’icône de clé qui apparaît lorsque vous pointez sur le compte d’Holly) afin de corriger son mot de passe.

18. Sélectionnez **Fermer**.

19. Restez connecté à la machine virtuelle Client 1 (LON-CL1) avec le Centre d’administration Microsoft 365 ouvert dans votre navigateur pour la tâche suivante.


### Tâche 2 : mettre à jour le groupe de projets pilotes Microsoft 365

Une fois la tâche précédente terminée, vous devriez toujours être connecté au **Centre d’administration Microsoft 365** sous le compte **Administrateur MOD**. Durant cette tâche, vous allez commencer à implémenter le projet pilote Microsoft 365 d’Adatum en tant qu’Holly Dickson, la nouvelle administratrice Microsoft 365 d’Adatum. Par conséquent, vous commencerez cette tâche en vous déconnectant de Microsoft 365 en tant qu’Administrateur MOD et en vous reconnectant à l’aide du compte d’Holly. 

Dans une tâche précédente, vous avez créé un groupe Microsoft 365 pour les membres de l’équipe Projet pilote d’Adatum afin de pouvoir créer un thème personnalisé pour ce groupe. Dans cette tâche, vous allez ajouter Holly à ce groupe. 

1. Sur la machine virtuelle LON-CL1, le **Centre d’administration Microsoft 365** doit toujours être ouvert dans votre navigateur Microsoft Edge suite à la tâche précédente. Vous devez être connecté à Microsoft 365 en tant qu’**Administrateur MOD**. <br/>

    Sur l’onglet **Centre d’administration Microsoft 365**, dans le coin supérieur droit de l’écran, notez la présence du nom de l’Administrateur MOD et d’une icône de mégaphone. La présence du nom est due au thème personnalisé que vous avez créé dans l’exercice de labo précédent, qui a été associé à un groupe d’utilisateurs de projet pilote Microsoft 365 incluant l’Administrateur MOD. Gardez cela à l’esprit lorsque vous vous reconnecterez en tant que Holly Dickson. <br/>

    Sélectionnez l’icône utilisateur ou le cercle avec les initiales « MA » pour **Administrateur MOD** dans le coin supérieur droit de votre navigateur. Dans la fenêtre **Administrateur MOD** qui s’affiche, sélectionnez **Se déconnecter**. <br/>
    
    **Important :** Lors du basculement d’un compte d’utilisateur vers un autre, vous devez fermer tous vos onglets de navigateur à l’exception de l’onglet **Se déconnecter**. Il s’agit d’une meilleure pratique qui permet d’éviter toute confusion grâce à la fermeture des fenêtres associées à l’utilisateur précédent. Une fois que vous êtes déconnecté du compte Administrateur MOD, fermez tous les autres onglets du navigateur, à l’exception de l’onglet **Se déconnecter**. 
    
2. Dans votre navigateur Microsoft Edge, sous l’onglet **Se déconnecter**, entrez l’URL suivante dans la barre d’adresse pour vous reconnecter à Microsoft 365 : **https://portal.office.com**. 

3. Dans la fenêtre **Choisir un compte**, seul le compte d’administrateur du locataire d’Administrateur MOD (le compte admin@xxxxxZZZZZZ.onmicrosoft.com) que vous venez de déconnecter est visible. Sélectionnez **Utiliser un autre compte**. 

4. Dans la fenêtre **Se connecter**, entrez **Holly@xxxxxZZZZZZ.onmicrosoft.com** (où xxxxxZZZZZZ est le préfixe de locataire fourni par votre fournisseur d’hébergement de labo). Cliquez sur **Suivant**.

5. Dans la fenêtre **Entrer le mot de passe**, entrez le nouveau mot de passe administratif que vous avez affecté au compte de Holly, puis sélectionnez **Se connecter**. 

6. Si une boîte de dialogue **Rester connecté ?** s’affiche, cochez la case **Ne plus afficher**, puis sélectionnez **Oui**. 

7. Si une boîte de dialogue **Bienvenue dans Microsoft 365** s’affiche au milieu de l’écran, il n’existe aucune option pour la fermer. Au lieu de cela, à droite de la fenêtre, sélectionnez deux fois l’icône de flèche vers l’avant (**>**), puis sélectionnez l’icône de coche pour parcourir les diapositives de cette fenêtre de message. 

8. Si une fenêtre **Créer avec Microsoft 365** s’affiche, sélectionnez le **X** dans le coin supérieur de la fenêtre pour la fermer. 

9. La page **Bienvenue dans Microsoft 365** s’affiche dans votre navigateur Edge sous l’onglet **Accueil | Microsoft 365**. Il s’agit de la page d’accueil Microsoft 365 d’Holly. Notez que les initiales d’Holly apparaissent dans le coin supérieur droit de l’écran ; en revanche, son nom n’est pas affiché. Cela est dû au fait que le compte d’Holly n’existait pas au moment où vous avez ajouté les utilisateurs du projet pilote Microsoft 365 au groupe associé au thème personnalisé dans l’exercice de labo précédent. Étant donné qu’Holly souhaite voir son nom en haut de chaque fenêtre Microsoft 365 lorsqu’elle est connectée au système, elle souhaite d’abord ajouter son compte au groupe d’utilisateurs du projet pilote Microsoft 365. <br>

    Dans la colonne des icônes d’application dans le volet de navigation sur le côté de l’écran, sélectionnez **Administrateur**. Cela ouvre le **Centre d’administration Microsoft 365** dans un nouvel onglet de navigateur. 

10. Dans le **Centre d’administration Microsoft 365**, sélectionnez **Équipes + groupes** dans le volet de navigation et, en dessous, sélectionnez **Équipes et groupes actifs**. 

11. Dans la page **Équipes et groupes actifs** figure un onglet permettant d’afficher chacun des types de groupes. L’onglet **Groupes Teams et Microsoft 365** est affiché par défaut. Sous cet onglet, sélectionnez **Projet pilote M365**.

12. Dans le volet **Projet pilote M365** qui s’affiche, l’onglet **Général** est affiché par défaut. Sélectionnez l’onglet **Appartenance**.

13. Sous l’onglet **Appartenance**, le sous-onglet **Propriétaires** s’affiche par défaut dans le volet de navigation sur le côté du volet. Sélectionnez le sous-onglet **Membres** qui apparaît en dessous.

14. Dans le sous-onglet **Membres**, sélectionnez **+Ajouter des membres**.

15. Dans le volet **Ajouter des membres de groupe à Projet pilote M365** qui s’affiche, sélectionnez à l’intérieur du champ **Rechercher par nom ou adresse de messagerie**. Dans la liste des utilisateurs qui s’affiche, faites défiler vers le bas et sélectionnez **Holly Dickson**. Sélectionnez le bouton **Ajouter (1)**, puis fermez le volet **Ajouter des membres de groupe à Projet pilote M365** une fois qu’Holly a été ajoutée au groupe.

16. Restez connecté à LON-CL1 avec le **Centre d’administration Microsoft 365** ouvert dans votre navigateur pour la tâche suivante.


### Tâche 3 : Créer une stratégie d’accès conditionnel pour implémenter la MFA

Comme indiqué dans votre formation, il existe trois manières d’implémenter MFA : avec des stratégies d’accès conditionnel, avec des paramètres de sécurité par défaut, et avec l’authentification multifacteur héritée par utilisateur (non recommandée pour les grandes organisations). Dans cet exercice, vous allez activer MFA par le biais d’une stratégie d’accès conditionnel, ce qui est la méthode recommandée par Microsoft. 

Adatum a chargé Holly d’activer la MFA pour tous ses utilisateurs Microsoft 365, à la fois internes et externes. Toutefois, pour tester l’implémentation du projet pilote Microsoft 365 d’Adatum, Holly souhaite faire en sorte que les membres du groupe de projet pilote M365 ne soient pas obligés d’utiliser MFA pour se connecter. Une fois le projet pilote terminé, Holly compte mettre à jour la stratégie en supprimant l’exclusion de ce groupe de l’exigence d’authentification multifacteur. La stratégie inclura également deux autres exigences. Elle exigera MFA pour toutes les applications cloud, même si un utilisateur se connecte à partir d’une localisation approuvée. 

1. Sur la machine virtuelle LON-CL1, le **Centre d’administration Microsoft 365** devrait encore être ouvert dans votre navigateur Microsoft Edge suite à une tâche précédente. Vous devez être connecté à Microsoft 365 en tant que **Holly Dickson**.
   
2. Dans le **Centre d’administration Microsoft 365**, dans la section **Centres d’administration** du volet de navigation, sélectionnez **Identité**. Cela ouvre le centre d’administration Microsoft Entra dans un nouvel onglet de navigateur. Dans la fenêtre **Choisir un compte** qui s’affiche, sélectionnez le **compte d’Holly Dickson**.

3. Dans le **centre d’administration Microsoft Entra**, sélectionnez **Protection** dans le volet de navigation, puis **Accès conditionnel**.

4. Sur la page **Accès conditionnel | Vue d’ensemble**, sélectionnez **Stratégies** dans le volet de navigation central.

5. Sur la page **Accès conditionnel | Stratégies**, dans la barre de menus en haut de la page, sélectionnez **+Créer une stratégie**.

6. Dans la fenêtre **Nouvelle stratégie d’accès conditionnel**, entrez **MFA pour tous les utilisateurs Microsoft 365** dans le champ **Nom**.

7. Vous commencerez par définir l’exigence MFA pour les utilisateurs. Sous le groupe **Utilisateurs**, sélectionnez **0 utilisateurs et groupes sélectionnés**. Cela affiche deux onglets : **Inclure** et **Exclure**.

8. Sous l’onglet **Inclure**, sélectionnez **Tous les utilisateurs**. Notez le message d’avertissement qui s’affiche. Vous allez réagir à cet avertissement lors des deux étapes suivantes.

9. Sélectionnez l’onglet **Exclure**. Pour éviter le verrouillage système, comme indiqué dans le message d’avertissement précédent, vous souhaitez exclure vos Administrateurs généraux (en l’occurrence, Holly). Holly souhaite également exclure les autres membres du groupe de projet pilote Microsoft 365 pour des raisons de rapidité lors des tests. Une fois Microsoft 365 en ligne chez Adatum, Holly supprimera le groupe de projets pilotes de la liste Exclure dans cette stratégie d’accès conditionnel, et s’exclura simplement elle-même, l’Administrateur MOD et quelques autres Administrateurs généraux. Mais pour l’instant, Holly veut exclure l’ensemble du groupe de projets pilotes. <br/>

    Pour ce faire, cochez la case **Utilisateurs et groupes**. 

10. Dans la fenêtre **Sélectionner des utilisateurs et des groupes exclus** qui s’affiche, vous sélectionnerez le groupe de projets pilotes Microsoft 365. L’onglet **Tous** s’affiche par défaut. Pour trouver rapidement le groupe de projet pilote, sélectionnez l’onglet **Groupes**. Dans la liste des groupes actifs, cochez la case en regard du groupe **Projet pilote M365**, puis sélectionnez le bouton **Sélectionner** en bas de la fenêtre. De retour dans la fenêtre **Nouvelle stratégie d’accès conditionnel**, notez le message qui s’affiche dans la section **Utilisateurs**. 

11. Vous allez maintenant définir l’exigence MFA pour toutes les applications cloud. Dans la section **Ressources cibles**, sélectionnez **Aucune ressource cible sélectionnée**. Cela affiche deux onglets : **Inclure** et **Exclure**.

12. Sélectionnez le champ déroulant **Sélectionner à quoi cette stratégie s’applique** pour afficher les différentes options du menu déroulant. Sélectionnez **Ressources (anciennement applications cloud)**. 

13. Sous l’onglet **Inclure**, notez que le paramètre par défaut est **Aucune**. Si vous n’aviez pas modifié ce paramètre, aucune application cloud (y compris Microsoft 365) n’exigerait la MFA. Ainsi, même si vous aviez créé cette stratégie et sélectionné l’option pour exiger la MFA de tous les utilisateurs, mais que vous aviez conservé la valeur de **Ressources cibles** sur **Aucune**, aucun utilisateur se connectant à Microsoft 365 ne serait obligé d’utiliser la MFA. <br/>

    Dans l’onglet **Inclure**, sélectionnez l’option **Sélectionner les ressources**. Cette opération affiche deux sections : **Modifier le filtre** et **Sélectionner**. Dans la section **Sélectionner**, sélectionnez **Aucun**. 

14. Dans le volet **Sélectionner des ressources** qui s’affiche, faites défiler la liste des applications afin d’afficher toutes les différentes applications pour lesquelles vous pourriez avoir besoin de l’authentification multifacteur. **Ne sélectionnez AUCUNE des applications.** Nous vous demandons de faire défiler cette liste simplement pour que vous puissiez constater le degré de précision que vous pouvez appliquer lorsque vous exigez la MFA, dans le cas où vous décideriez de limiter MFA à certaines applications dans vos déploiements réels.  <br/>

    Pour Adatum, Holly souhaite exiger MFA pour toutes les applications cloud, ce qui est généralement un scénario métier plus courant que la sélection d’applications spécifiques. Dans l’onglet **Inclure**, sélectionnez l’option **Toutes les ressources (anciennement « Toutes les applications cloud »)**. Adatum n’exclura aucune application cloud de l’authentification MFA. Vous pouvez sélectionner l’onglet **Exclure** si vous souhaitez afficher les options proposées. Il fonctionne essentiellement de la même façon que l’onglet **Inclure**. Vous pouvez afficher cet onglet, mais ne sélectionnez aucune application cloud pour l’exclusion. 

15. Pour finir, vous allez définir l’exigence MFA pour toutes les localisations de connexion utilisateur. Dans certains scénarios, il se peut que les organisations exigent MFA uniquement si un utilisateur se connecte à partir d’une localisation non approuvée. Toutefois, Adatum souhaite exiger la MFA pour tous les utilisateurs inclus, indépendamment de l’endroit d’où ils se connectent. <br/>

    Sous **Conditions**, sélectionnez **0 condition sélectionnée**. Cette opération affiche une liste des conditions potentielles que la stratégie vérifiera. Pour cet exercice de labo, sous la condition **Localisations**, sélectionnez **Non configuré**. Cette opération affiche un bouton bascule **Configurer** et deux onglets, **Inclure** et **Exclure**. Les deux onglets sont actuellement désactivés.

16. Définissez le bouton bascule **Configurer** sur **Oui** afin d’activer les deux onglets. 

17. Sous l’onglet **Inclure**, vérifiez que l’option **Tous les réseaux ou emplacements** est sélectionnée (sélectionnez-la si nécessaire). Sélectionnez l’onglet **Exclure**. Si votre organisation reconnaît des adresses IP ou des plages d’adresses spécifiques comme étant « approuvées », vous pouvez exclure l’exigence MFA si un utilisateur se connecte à partir de l’une de ces localisations. Toutefois, Adatum souhaite exiger la MFA pour toutes les tentatives de connexion utilisateur, quelle que soit leur localisation. Cela comprend les connexions des utilisateurs internes et externes. Vérifiez que l’option **Réseaux et emplacements sélectionnés** est sélectionnée, et sous la section **Sélectionner**, vérifier que **Aucun** est indiqué. En ne spécifiant aucun emplacement sélectionné, ce paramètre garantit qu’aucun emplacement n’est exclu de MFA. 

18. Dans la section **Contrôles d’accès**, dans le groupe **Octroyer**, sélectionnez **0 contrôles sélectionnés**. Un volet **Octroyer** s’affiche.

19. Dans le volet **Octroyer** qui s’affiche, vérifiez que l’option **Autoriser l’accès** est sélectionnée (sélectionnez-la si nécessaire). Notez tous les contrôles d’accès disponibles qui peuvent être activés avec cette stratégie. Cette stratégie ne nécessitera que la MFA, vous devez donc cocher la case **Exiger l’authentification multifacteur**. Sélectionnez le bouton **Sélectionner** en bas du volet **Octroyer** afin de fermer le volet. 

20. En bas de la fenêtre **Nouvelle stratégie d’accès conditionnel**, dans le champ **Activer la stratégie**, sélectionnez **On**.

21. Notez le message d’avertissement et les options qui s’affichent en bas de la page, qui vous avertissent de ne pas vous verrouiller vous-même. Sélectionnez l’option **Je comprends que mon compte sera affecté par cette stratégie. Continuer malgré tout.** En fait, Holly ne sera pas affectée, car elle est membre du groupe de projet pilote M365, qui est exclu de cette stratégie.

22. Sélectionnez le bouton **Créer** pour créer la stratégie.

23. Dans la fenêtre **Accès conditionnel | Stratégies** qui s’affiche, vérifiez que la stratégie **MFA pour tous les utilisateurs Microsoft 365** s’affiche et que son **État** est **Activée**.

24. Restez connecté à LON-CL1 avec tous vos onglets de navigateur Microsoft Edge ouverts pour la tâche suivante.


### Tâche 4 : Tester MFA pour un utilisateur inclus et un utilisateur exclu

Pour tester la stratégie d’accès conditionnel que vous venez de créer, vous allez vous déconnecter de Microsoft 365 en tant que Holly, puis vous reconnecter en tant qu’Adele Vance. Adele n’est pas membre du groupe de projet pilote M365. Microsoft Entra devrait donc exiger qu’elle utilise MFA lors de la connexion. Après vous être connecté en tant qu’Adele et avoir vérifié le bon fonctionnement de MFA, vous vous déconnecterez en tant qu’Adele, puis vous vous reconnecterez en tant qu’Holly. Holly étant membre du groupe de projet pilote M365 qui a été exclu de l’utilisation de MFA dans la stratégie d’accès conditionnel, vous ne devriez pas avoir à utiliser MFA lors de la connexion en tant qu’Holly. De même, vous n’aurez pas besoin d’utiliser la MFA lorsque vous vous connecterez en tant que membres du groupe de projets pilotes M365 dans les labos restants de ce cours.

**Important :** Pour implémenter la MFA, vous devez utiliser votre téléphone mobile afin de recevoir un code de vérification, que vous entrerez dans votre tenant en guise de deuxième forme d’authentification. Si vous n’avez pas de téléphone, vous pouvez quand même tester votre stratégie d’accès conditionnel. Pour les étudiants sans téléphone, lorsque vous vous connecterez en tant qu’Adele Vance, le système vous oblige à vous connecter avec une deuxième forme d’authentification. À ce stade, vous pouvez simplement annuler votre connexion, puis vous reconnecter en tant qu’Holly, pour qui MFA ne sera pas nécessaire. Même si vous ne finalisez pas la connexion MFA pour Adele, vous pouvez néanmoins vérifier que le système vous oblige à l’utiliser lors de la tentative de connexion.

1. Sur la machine virtuelle LON-CL1, le **Centre d’administration Microsoft 365** doit toujours être ouvert dans votre navigateur Microsoft Edge suite à la tâche précédente. Vous devez être connecté à Microsoft 365 en tant que **Holly Dickson**. Vous allez commencer par vous déconnecter de Microsoft 365. Sous l’onglet **Centre d’administration Microsoft 365**, sélectionnez le nom d’Holly dans le coin supérieur droit de votre navigateur. Dans la fenêtre **Holly Dickson** qui s’affiche, sélectionnez **Se déconnecter**. 
    
2. Une fois que vous êtes déconnecté de Microsoft 365 en tant que Holly, fermez votre session de navigateur pour effacer votre cache. Sélectionnez ensuite l’icône **Edge** dans votre barre des tâches pour ouvrir une nouvelle session de navigateur. Dans votre navigateur, accédez à la page **Accueil Microsoft 365** en entrant l’URL suivante dans la barre d’adresse : **https://portal.office.com/** 

3. Dans la fenêtre **Choisir un compte** qui s’affiche, sélectionnez **Utiliser un autre compte**. 

4. Dans la fenêtre **Se connecter**, entrez **AdeleV@xxxxxZZZZZZ.onmicrosoft.com** (où xxxxxZZZZZZ est le préfixe de locataire fourni par votre fournisseur d’hébergement de labo), puis sélectionnez **Suivant**. Dans la fenêtre **Entrer un mot de passe**, entrez le **mot de passe utilisateur** fourni par votre fournisseur d’hébergement de labo, puis sélectionnez **Se connecter**.

5. MFA étant activé pour tous les utilisateurs sauf les membres du groupe de projet pilote M365 (dont Adele n’est pas membre), une fenêtre **Plus d’informations requises** s’affiche. Cliquez sur **Suivant**. Cela provoque l’affichage de la page **Microsoft Authenticator**, qui constitue le point de départ de la connexion avec MFA. <br/>

    **Important :** Si vous n’avez pas de téléphone, vous ne pourrez pas aller plus loin dans le processus de connexion en tant qu’Adele. Même si vous ne pouvez pas terminer la connexion, vous avez confirmé que la première partie de votre stratégie d’accès conditionnel fonctionnait, car elle exige qu’Adele se connecte à l’aide de MFA. À ce stade, passez à l’étape 18 pour pouvoir vous reconnecter en tant que Holly.

6. Dans la page **Microsoft Authenticator** qui s’affiche, vous pouvez télécharger cette application mobile ou utiliser une autre méthode pour la vérification MFA. Pour les besoins de ce labo, nous vous recommandons d’utiliser votre téléphone mobile afin de ne pas avoir à installer l’application Microsoft Authenticator, que vous n’utiliserez peut-être plus après ce cours de formation. Sélectionnez l’option **Je veux configurer une autre méthode** en bas de la page (**Important :** Ne confondez PAS ce lien avec le lien **Je souhaite utiliser une autre application d’authentification** qui se trouve au-dessus). 

7. Dans la boîte de dialogue **Choisir une autre méthode** qui s’affiche, sélectionnez la flèche déroulante dans le champ **Quelle méthode voulez-vous utiliser ?**, sélectionnez **Téléphone**, puis sélectionnez **Confirmer**. 

8. Dans la fenêtre **Téléphone** qui s’affiche, dans le champ **Quel numéro de téléphone voulez-vous utiliser ?**, sélectionnez votre pays ou région puis, dans le champ à côté de celui-ci, saisissez votre numéro de téléphone (selon le format spécifique à votre pays). Vérifiez que l’option **Recevoir un code** est sélectionnée, puis sélectionnez **Suivant**.

9. Récupérez le code de vérification à partir du SMS envoyé à votre téléphone.

10. Dans la fenêtre **Téléphone**, entrez le code de vérification à six chiffres dans le champ de code, puis sélectionnez **Suivant**. Lorsque la fenêtre **Téléphone** affiche un message indiquant que votre téléphone a été enregistré avec succès, sélectionnez **Suivant**.

11. Dans la page **Opération réussie**, sélectionnez **Terminé**.

12. Microsoft a implémenté une nouvelle stratégie de sécurité dans les tenants d’évaluation utilisés dans ses labos de formation. Tous les comptes d’utilisateur de test prédéfinis sont configurés afin que les étudiants puissent modifier leur mot de passe initial lors de leur prochaine connexion. Vous devez le faire maintenant avec Adele. <br>

    Dans la fenêtre **Mettre à jour votre mot de passe** qui s’affiche, entrez le **Mot de passe de l'utilisateur** fourni par votre fournisseur d’hébergement de labo dans le champ **Mot de passe actuel**. Ensuite, dans les champs **Nouveau mot de passe** et **Confirmer le mot de passe**, entrez le nouveau mot de passe de l’utilisateur que vous avez défini pour tous les utilisateurs de test au début du labo. Cliquez sur **Connexion**.

13. Si une boîte de dialogue **Rester connecté ?** s’affiche, cochez la case **Ne plus afficher**, puis sélectionnez **Oui**. 

14. Si une boîte de dialogue **Bienvenue dans Microsoft 365** s’affiche, cochez la flèche droite deux fois, puis sélectionnez la coche.

15. Si une fenêtre **Créer avec Microsoft 365** s’affiche, sélectionnez le **X** pour la fermer.

16. Sur la page **Bienvenue dans Microsoft 365**, sélectionnez l’icône du **Lanceur d’applications**, puis sélectionnez **Word**. Cela ouvre **Microsoft Word Online**. Cela confirme que vous pouvez accéder à une application Microsoft 365 après vous être connecté à l’aide de MFA.  <br/>

    **Important :** Vous avez maintenant vérifié que la première partie de la stratégie d’accès conditionnel que vous avez créée fonctionne. La stratégie impose qu’un utilisateur qui n’est pas membre de l’équipe de projet pilote Microsoft 365 se connecte à l’aide de MFA. Vous avez vérifié que cela fonctionnait lorsque vous vous êtes connecté en tant qu’Adele. Vous allez maintenant vous déconnecter en tant qu’Adele et vous reconnecter en tant qu’Holly, afin de vérifier que la deuxième partie de la stratégie d’accès conditionnel fonctionne également. Vous ne devriez PAS avoir à utiliser MFA lors de la connexion en tant qu’Holly, puisqu’elle est membre du groupe de projet pilote M365, qui est exclu de l’exigence MFA dans la stratégie d’accès conditionnel.

17. Sous l’onglet **Centre d’administration Microsoft 365**, sélectionnez l’icône du compte d’Holly dans le coin supérieur droit de votre navigateur. Dans la fenêtre **Adele Vance** qui s’affiche, sélectionnez **Se déconnecter**. <br/>
    
18. Fermez votre session de navigateur pour effacer votre cache. Sélectionnez l’icône **Edge** dans votre barre des tâches pour ouvrir une nouvelle session de navigateur. Dans votre navigateur, accédez à la page **Accueil Microsoft 365** en entrant l’URL suivante dans la barre d’adresse : **https://portal.office.com/** 

19. Dans la fenêtre **Choisir un compte**, sélectionnez **Holly@xxxxxZZZZZZ.onmicrosoft.com** (où xxxxxZZZZZZ est le préfixe de locataire fourni par votre fournisseur d’hébergement de labo), puis **Suivant**. Dans la fenêtre **Entrer le mot de passe**, entrez le nouveau mot de passe d’administration que vous avez défini pour tous les utilisateurs de test au début du labo, puis affecté au compte de Holly. Cliquez sur **Connexion**.

20. L’authentification MFA étant requise pour tous les utilisateurs sauf les membres de l’équipe de projet pilote M365 (dont Holly est membre), elle ne sera pas obligatoire ici. La MFA n’étant pas requise, le système affiche la page **Accueil Microsoft 365** dans l’onglet ** Accueil | Microsoft 365** . 

21. Si une boîte de dialogue **Bienvenue dans Microsoft 365** s’affiche, cochez la flèche droite deux fois, puis sélectionnez la coche.

22. Si une fenêtre **Créer avec Microsoft 365** s’affiche, sélectionnez le **X** pour la fermer.

23. Sur la page **Bienvenue dans Microsoft 365**, sélectionnez l’icône **Administrateur** dans le volet latéral pour accéder au **Centre d’administration Microsoft 365**. <br/>

    **Important :** Vous avez maintenant vérifié que la deuxième partie de la stratégie d’accès conditionnel que vous avez créée fonctionne. La stratégie exclut les membres du groupe de projet pilote Microsoft 365 de l’obligation de se connecter à l’aide de MFA. Holly est membre de ce groupe, et elle n’a pas été contrainte de se connecter à l’aide de MFA.

24. Restez connecté à LON-CL1 avec le **Centre d’administration Microsoft 365** ouvert dans votre navigateur.


### Tâche 5 : Déployer le verrouillage intelligent Microsoft Entra

Le Directeur technique d’Adatum vous a demandé de déployer le verrouillage intelligent Microsoft Entra, qui aide à bloquer les acteurs malveillants qui essaient de deviner les mots de passe de vos utilisateurs ou d’utiliser des méthodes de force brute pour être admis dans votre réseau. Le verrouillage intelligent peut reconnaître les connexions provenant d’utilisateurs validés, et les traiter différemment de celles des attaquants et autres sources inconnues. 

Le Directeur technique tient beaucoup à l’implémentation du verrouillage intelligent, car il empêchera les attaquants de pénétrer dans le système, tout en permettant aux utilisateurs d’Adatum de continuer à accéder à leurs comptes et de travailler. Le Directeur technique a demandé à Holly de configurer le verrouillage intelligent afin que les utilisateurs ne puissent pas utiliser le même mot de passe plusieurs fois et qu’ils ne puissent pas utiliser de mots de passe considérés comme trop simplistes ou courants. 

**Remarque :** Vous pouvez tenir à jour les paramètres de stratégie de verrouillage de compte dans l’Éditeur de gestion des stratégies de groupe et dans Microsoft Entra par le biais de sa fonctionnalité de verrouillage intelligent. Cette tâche de labo montre comment accéder à chaque méthode, mais vous mettrez à jour les paramètres de verrouillage intelligent uniquement dans Microsoft Entra. Vous devez utiliser le contrôleur de domaine de l’entreprise (LON-DC1) pour accéder à l’Éditeur de gestion des stratégies de groupe. 

1. Sur LON-DC1, sélectionnez l’icône du **Gestionnaire de serveur** dans la barre des tâches si celui-ci est déjà ouvert. Sinon, ouvrez-le maintenant.

2. Dans le **Gestionnaire de serveur**, sélectionnez **Outils** dans la barre de menus en haut à droite puis, dans le menu déroulant, sélectionnez **Gestion des stratégies de groupe**.

3. Agrandissez la fenêtre **Gestion des stratégies de groupe**.

4. Vous souhaitez modifier la stratégie de groupe qui inclut la stratégie de verrouillage de compte de votre organisation. Si nécessaire, dans l’arborescence de la console racine dans le volet latéral, développez **Forest:Adatum.com**, **Domaines**, puis **Adatum.com**.  <br/>

    Sous **Adatum.com**, cliquez avec le bouton droit sur **Stratégie de domaine** par défaut, puis sélectionnez **Modifier** dans le menu.

5. Agrandissez la fenêtre **Éditeur de gestion des stratégies de groupe** qui s’affiche.

6. Dans l’arborescence **Domaine par défaut Azure Policy** dans le volet latéral, sous **Configuration ordinateur**, développez **Stratégies**, **Paramètres Windows**, **Paramètres de sécurité**, puis **Stratégies de compte**.

7. Dans le dossier **Stratégies de compte**, sélectionnez **Stratégie de verrouillage de compte**.

8. Comme vous pouvez le voir dans le volet de détails situé au milieu, aucun paramètre de verrouillage intelligent n’a été défini. Au lieu de tenir à jour ces paramètres de verrouillage dans l’Éditeur de gestion des stratégies de groupe, vous allez utiliser le Centre d’administration Microsoft Entra. Bien que vous puissiez utiliser l’Éditeur de gestion des stratégies de groupe, cette méthode est généralement utilisée dans les environnements Active Directory locaux. Nous vous avons montré cet éditeur afin que vous sachiez que cette alternative existe. Toutefois, pour les organisations qui utilisent strictement des services cloud tels que Microsoft 365 ou qui trouvent l’utilisation du centre d’administration Microsoft Entra beaucoup plus conviviale que l’accès à l’Éditeur de gestion des stratégies de groupe, l’utilisation du **centre d’administration Microsoft Entra** pour attribuer des valeurs correspondantes dans le contexte Entra ID est préférable. <br/>  

    Sachez également que le comportement de verrouillage et les options de personnalisation diffèrent entre les deux méthodes. Avec l’Éditeur de gestion des stratégies de groupe, vous avez un contrôle plus précis sur les paramètres de stratégie, notamment Seuil de verrouillage, Durée du verrouillage et Réinitialiser le compteur de verrouillage du compte au bout de. Toutefois, l’application de cette méthode nécessite une connaissance de la stratégie de groupe et de l’administration Active Directory. À l’inverse, la stratégie de verrouillage de compte dans Microsoft Entra ne peut pas être personnalisée de manière aussi étendue. En revanche, elle est plus facile à utiliser, même si elle n’offre pas certaines des options de réglage fin disponibles dans Stratégie de groupe. <br/>

    Pour Adatum, Holly a choisi d’utiliser le centre d’administration Microsoft Entra pour configurer la stratégie de verrouillage de compte de l’entreprise. Dans la barre des tâches en bas de votre écran, sélectionnez l’icône de **Microsoft Edge**, qui doit afficher le **centre d’administration Microsoft Entra**. 

9. Dans le **centre d’administration Microsoft Entra**, sélectionnez **Protection** dans le volet de navigation, puis **Méthodes d’authentification**. 

10. Dans la page **Méthodes d’authentification | Stratégies**, dans le volet central, dans la section **Gérer**, sélectionnez **Protection par mot de passe**.

11. Dans la fenêtre **Méthodes d’authentification | Protection par mot de passe**, dans le volet de détails à droite, entrez les informations suivantes :

    - Dans la section **Verrouillage intelligent personnalisé** :

        - **Seuil de verrouillage** : ce champ indique le nombre d’échecs de connexion autorisés avant qu’un compte ne soit verrouillé. La valeur par défaut est de 10. À des fins de test, Adatum vous a demandé d’affecter la valeur **3** à ce paramètre.

        - **Durée du verrouillage en secondes** : il s’agit de la durée en secondes de chaque verrouillage. La valeur par défaut est 60 secondes (une minute). Adatum vous a demandé de régler ce paramètre sur **90** secondes.

    - Dans la section **Mots de passe interdits personnalisés** :

        - **Appliquer la liste personnalisée** : sélectionnez **Oui**

        - **Liste de mots de passe interdits personnalisés :** entrez les valeurs suivantes (appuyez sur Entrée après avoir entré chaque valeur, afin qu’elles se trouvent sur des lignes distinctes) :

            - **Password01**

            - **F00tball01**

            - **Se@Hawks1**

            - **Never4get!!**

    - Dans la section **Mode**, sélectionnez **Appliqué**.

12. Sélectionnez **Enregistrer** dans la barre de menus en haut de la page.

13. Vous devez maintenant tester la fonctionnalité de mot de passe interdit. Sélectionnez l’icône utilisateur d’Holly Dickson dans le coin supérieur droit de l’écran puis, dans le menu qui s’affiche, sélectionnez **Afficher le compte**. 

14. Dans la fenêtre **Mon compte** qui s’affiche, dans la vignette **Mot de passe**, sélectionnez** MODIFIER LE MOT DE PASSE**.

15. Un nouvel onglet s’ouvre et affiche la fenêtre **Modifier le mot de passe**. Dans le champ **Ancien mot de passe**, entrez le mot de passe existant de Holly, qui est le nouveau mot de passe d’administration. <br/>

    Entrez **Never4get !!** dans les champs **Créer un mot de passe** et **Confirmer le nouveau de mot de passe**, puis sélectionnez **Envoyer**. Notez le message d’erreur que vous recevez.

16. Dans votre navigateur, fermez l’onglet **Modifier le mot de passe**. 

17. Vous allez maintenant tester la fonctionnalité de seuil de verrouillage. Vous allez le faire à l’aide du compte Adele Vance. Sélectionnez l’icône utilisateur d’Holly Dickson dans le coin supérieur droit de l’écran puis, dans le menu qui s’affiche, sélectionnez **Se déconnecter**.  

18. Une fois que vous êtes déconnecté en tant qu’Holly, la fenêtre **Choisir un compte** s’affiche sous l’onglet **Se connecter à Microsoft Entra**. En guise de meilleure pratique lors de la déconnexion d’un service en ligne Microsoft et du basculement d’un utilisateur vers un autre, fermez tous vos onglets de navigateur sauf l’onglet **Se déconnecter** ou **Se connecter**. Dans le cas présent, fermez les autres onglets maintenant et laissez l’onglet **Se connecter** ouvert.  <br/>

    Dans la fenêtre **Choisir un compte**, sélectionnez **Utiliser un autre compte**. 

19. Dans la fenêtre **Se connecter**, entrez **adelev@xxxxxZZZZZZ.onmicrosoft.com** (où xxxxxZZZZZZ est le préfixe de tenant fourni par votre fournisseur d’hébergement de labo), puis sélectionnez **Suivant**. 

20. Dans la fenêtre **Entrer un mot de passe**, entrez une combinaison aléatoire de lettres et de chiffres, puis sélectionnez **Se connecter**. Notez le message d’erreur de mot de passe non valide qui s’affiche. 

    Répétez cette étape deux autres fois. 
    
    Étant donné que vous avez défini le **Seuil de verrouillage** sur **3**, vous devez recevoir un message d’erreur indiquant que ce compte est verrouillé après la troisième tentative de connexion ayant échoué. <br/>

    **Remarque :** Si vous ne recevez pas ce message de verrouillage après la troisième tentative, cela signifie que le système n’a pas encore fini de propager ce seuil de verrouillage dans tout le service. Les modifications seront effectives après quelques minutes. Patientez quelques minutes, puis reconnectez-vous avec un mot de passe incorrect. Les tests de ce labo ont entraîné des résultats variables. La modification se propage parfois presque immédiatement, auquel cas vous êtes verrouillé après la troisième tentative de connexion. D’autres fois, il a fallu entre cinq et dix minutes avant l’affichage du message de verrouillage. Continuez jusqu’à ce que vous receviez le message de verrouillage, après quoi le compte d’Adele sera temporairement verrouillé afin d’empêcher tout accès non autorisé.

21. Vous ne pourrez plus vous reconnecter en tant qu’Adele tant que la **durée de verrouillage de 90 secondes** que vous avez définie précédemment ne se sera pas écoulée. <br/>

    Une fois que vous avez été verrouillé, attendez 90 secondes, puis reconnectez-vous en tant que **adelev@xxxxxZZZZZZ.onmicrosoft.com** (où xxxxxZZZZZZ est le préfixe de locataire qui vous a été attribué par votre fournisseur d’hébergement de labo). Dans le champ **Mot de passe**, saisissez le mot de passe d’Adele, qui est le mot de passe utilisateur fourni par le fournisseur d’hébergement de votre labo. 

22. L’authentification multifacteur étant activée pour tous les utilisateurs, sauf les membres du groupe de projets pilotes M365 (dont Adele n’est pas membre), une fenêtre **Plus d’informations sont requises** s’affiche pour vous permettre de finaliser le processus d’authentification multifacteur pour Adele. Il s’agit de la vérification que votre tentative de connexion à l’aide du mot de passe réel d’Adele a réussi.  <br>

    **Remarque :** vous n’avez PAS besoin de finaliser le processus d’authentification multifacteur pour Adele, car il s’agit de votre dernier exercice de labo qui utilise le contrôleur de domaine LON-DC1. Vous pouvez fermer toutes les applications sur LON-DC1.

# Passer au labo 2 – Exercice 2
