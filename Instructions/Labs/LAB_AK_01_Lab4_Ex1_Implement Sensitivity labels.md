# Parcours d’apprentissage 1 - Labo 4 - Exercice 1 - Implémenter des étiquettes de confidentialité avec Protection Microsoft Entra ID

Jouant le rôle d’Holly Dickson, la nouvelle administratrice Microsoft 365 d’Adatum, vous avez déployé Microsoft 365 dans un environnement de laboratoire virtualisé. Les étapes suivantes de votre projet pilote Microsoft 365 consistent à implémenter chez Adatum des étiquettes de confidentialité avec la Protection des données Microsoft Purview. Dans ce labo, vous allez créer et publier une étiquette, puis vous testerez une étiquette publiée. Toutefois, ce faisant, vous ne testerez pas l’étiquette que vous créerez dans ce labo, Vous allez tester une étiquette différente.

**Important :** Lorsque vous publiez une nouvelle étiquette de confidentialité et une stratégie d’étiquette, la propagation via Microsoft 365 peut prendre jusqu’à 24 heures. Par conséquent, vous ne pourrez pas tester l’étiquette que vous créerez dans ce labo. Au lieu de cela, vous testerez une étiquette de confidentialité préexistante nommée **Project - Falcon**. Étant donné que cette étiquette préexistante est quasiment identique à l’étiquette que vous allez créer, vous allez pouvoir obtenir pratiquement les mêmes résultats qu’avec l’étiquette que vous avez créée si vous l’aviez testée. 


### Tâche 1 - Installer le client Protection des données Microsoft Purview

Pour implémenter des étiquettes de confidentialité dans le cadre de votre projet pilote chez Adatum, vous devez d’abord installer le **client Protection des données Microsoft Purview** à partir du Centre de téléchargement Microsoft.

1. À la fin du labo précédent, vous étiez sur LON-CL2. Basculez vers **LON-CL1**.  <br/>

    Vous devriez toujours être connecté à LON-CL1 avec le compte local **adatum\administrateur**, et dans votre navigateur Edge, vous devriez toujours être connecté à Microsoft 365 en tant que **Holly Dickson**. 

2. Dans **Microsoft Edge**, ouvrez un nouvel onglet et entrez (ou copiez et collez) l’URL suivante dans la barre d’adresse : **https://www.microsoft.com/en-us/download/confirmation.aspx?id=53018** <br/>

    Cette opération démarre le téléchargement pour le **client Protection des données Microsoft Purview**.

3. Dans la fenêtre **Téléchargements** qui s’affiche en haut à droite de la page, vous constaterez que le fichier **PurviewInfoProtection.exe** est en cours de téléchargement. Une fois le fichier téléchargé, sélectionnez le lien **Ouvrir le fichier** qui apparaît sous le nom de fichier.

4. L’Assistant **Microsoft Azure Information Protection** s’ouvrira. Si l’Assistant ne s’affiche pas sur le Bureau, sélectionnez l’icône de l’Assistant dans la barre des tâches pour l’afficher.

5. Dans l’assistant, dans la fenêtre **Installer le client Protection des données Microsoft Purview** qui s’affiche, cochez la case **Je reconnais que le complément AIP pour Office sera désinstallé (obligatoire)** et décochez la case **Aider à améliorer Protection des données Microsoft Purview en envoyant des statistiques d’utilisation à Microsoft**. Sélectionnez ensuite le bouton **J’accepte**.

6. Une fois l’installation terminée, sélectionnez **Fermer**.

Vous avez correctement installé le **client Protection des données Microsoft Purview** sur la machine virtuelle LON-CL1.


### Tâche 2 : activer les étiquettes de confidentialité pour les fichiers dans SharePoint et OneDrive

Dans cet exercice, vous activerez des étiquettes de confidentialité pour les fichiers Office et les fichiers PDF pris en charge dans SharePoint et OneDrive. Lorsque cette fonctionnalité est activée, les utilisateurs voient le bouton **Confidentialité** sur le ruban, afin de pouvoir appliquer des étiquettes. Ils voient également tout nom d’étiquette appliqué sur la barre d’état. Pour SharePoint, les utilisateurs peuvent également voir et appliquer des étiquettes de confidentialité depuis le volet d’informations.

L’activation de cette fonctionnalité permet en outre à SharePoint et OneDrive de traiter le contenu des fichiers Office et, éventuellement, des documents PDF chiffrés à l’aide d’une étiquette de confidentialité. L’étiquette peut être appliquée dans Office pour le web ou dans les applications de bureau Office, et téléchargée ou enregistrée dans SharePoint et OneDrive. Tant que vous n’activez pas cette fonctionnalité, ces services ne peuvent pas traiter les fichiers chiffrés, ce qui signifie que la co-création, la découverte électronique, la protection contre la perte de données, la recherche et d’autres fonctionnalités collaboratives ne fonctionneront pas pour ces fichiers.

Vous commencerez par activer les étiquettes de confidentialité pour les fichiers Office en ligne stockés dans SharePoint et OneDrive. Vous activerez ensuite la prise en charge des fichiers PDF.

**Remarque :** Comme pour toutes les modifications de configuration au niveau du tenant pour SharePoint et OneDrive, la modification met environ 15 minutes pour entrer en vigueur.

1. Sur LON-CL1, dans votre navigateur Edge, vous devez toujours être connecté à Microsoft 365 en tant que **Holly Dickson**.

2. Dans votre navigateur Edge, vous devez toujours avoir un onglet ouvert pour le **Centre d’administration Microsoft 365**. Si ce n’est pas le cas, ouvrez un nouvel onglet et entrez l’URL suivante : **https://admin.microsoft.com**.

3. Dans le **Centre d’administration Microsoft 365**, si nécessaire, sélectionnez **... Afficher tout**. Sélectionnez **Conformité** sous le groupe **Centres d’administration**. Cela ouvre le portail Microsoft Purview dans un nouvel onglet.

4. Vous commencerez en activant les étiquettes de confidentialité pour les fichiers Office en ligne stockés dans SharePoint et OneDrive. <br/>

    Dans le portail **Microsoft Purview**, dans la section **Solutions** du volet de navigation, sélectionnez **Protection des données**, puis **Étiquettes de confidentialité**.

5. Sur la page **Étiquettes de confidentialité**, le message suivant doit apparaître au milieu de la page : **Votre organisation n’a pas activé la possibilité de traiter du contenu dans des fichiers Office en ligne sur lesquels des étiquettes de confidentialité chiffrées sont appliquées et qui sont enregistrés dans OneDrive et SharePoint. Vous pouvez activer cette option ici, mais notez qu’une configuration supplémentaire est requise pour les environnements multigéographiques.** <br/>

    Sous ce message se trouve un bouton**Activer maintenant**. Sélectionnez ce bouton.  <br/>

    **Remarque :** La commande s’exécute immédiatement et lorsque la page sera actualisée, vous ne verrez plus le message ni le bouton.

6. Vous allez maintenant activer la protection PDF pour les fichiers dans SharePoint et OneDrive. <br/>

    Dans le portail **Microsoft Purview**, sous **Protection des informations** du volet de navigation, sélectionnez **Étiquetage automatique**.

7. Sur la page **Étiquetage automatique**, vous devez voir une bannière **Protéger les fichiers PDF avec l’étiquetage automatique** au milieu de la page. Sélectionnez le titre **Protéger les PDF avec l’étiquetage automatique** pour activer la protection PDF pour les fichiers dans SharePoint et OneDrive. 

8. Dans la boîte de dialogue **Stratégies à étiquetage automatique** qui s’affiche, sélectionnez **Confirmer** pour confirmer que vous souhaitez activer la protection PDF pour les fichiers dans SharePoint et OneDrive. 

    **Remarque :** La commande s’exécute immédiatement et lorsque la page sera actualisée, vous ne verrez plus la bannière **Protéger les PDF avec l’étiquetage automatique**.

9. Laissez votre navigateur Edge ouvert ainsi que tous les onglets. 


### Tâche 3 : créer une étiquette de confidentialité

Dans cet exercice, vous allez créer une étiquette de confidentialité et l’ajouter à la stratégie par défaut afin qu’elle soit valide pour tous les utilisateurs du locataire Adatum.

1. Sur LON-CL1, dans votre navigateur Edge, vous devez toujours être connecté à Microsoft 365 en tant que **Holly Dickson**.

2. Dans votre navigateur Edge, vous devez toujours avoir un onglet ouvert pour le portail **Microsoft Purview** de la tâche précédente. Dans le portail **Microsoft Purview**, dans le groupe **Protection des données** dans le volet de navigation, sélectionnez **Étiquettes de confidentialité**. 

3. Sur la page **Étiquettes de confidentialité**, sélectionnez l’option **+ Créer une étiquette** qui apparaît dans la barre de menu au milieu de l’écran. Cela lance l’Assistant **Nouvelle étiquette de confidentialité**.

4. Dans l’Assistant **Nouvelle étiquette de confidentialité**, dans la page **Fournir des détails de base pour cette étiquette**, entrez les informations suivantes :

    - Nom : **PII**
    
    - Nom complet : **PII**

    - Description pour les utilisateurs : **Documents, fichiers et e-mails avec informations d’identification personnelle**

    - Description pour les administrateurs : **Documents, fichiers et e-mails avec informations d’identification personnelle**

    - Couleur d’étiquette : sélectionnez l’une des couleurs que vous souhaitez affecter à vos étiquettes de confidentialité.

5. Cliquez sur **Suivant**.

6. Sur la page **Définir l’étendue de cette étiquette**, vérifiez que la case **Éléments** est cochée, ainsi que les cases **Fichiers**, **E-mails** et **Réunions** situées en dessous (cochez ces quatre cases si nécessaire). Ces cases à cocher vous permettent de définir l’emplacement où cette étiquette de confidentialité sera utilisée afin de pouvoir configurer les paramètres de protection applicables. Cliquez sur **Suivant**.

7. Sur la page **Choisir les paramètres de protection pour les types d’éléments sélectionnés**, vous pouvez commencer le processus d’utilisation des paramètres de chiffrement pour restreindre l’accès au contenu auquel l’étiquette sera appliquée. Lorsqu’un document, un e-mail ou une invitation à une réunion sont chiffrés, l’accès au contenu est restreint, de sorte que :  <br/>

    - il ne peut être déchiffré que par les utilisateurs autorisés désignés par les paramètres de chiffrement de l’étiquette.
    - le document reste chiffré, quel que soit son emplacement, qu’il soit à l’intérieur ou à l’extérieur de votre organisation, et ce même si le fichier est renommé ;
    - L’élément est chiffré au repos (par exemple, dans un compte OneDrive) et en transit (par exemple, un e-mail lors de son transfert sur internet).

   Holly souhaite configurer les paramètres de chiffrement. Par conséquent, sur la page **Choisir les paramètres de protection pour les types d’éléments sélectionnés**, cochez la case **Contrôler l’accès**. Cochez également la case **Appliquer le marquage de contenu** pour pouvoir configurer ultérieurement les paramètres d’en-tête, de pied de page et de filigrane. Cliquez sur **Suivant**.

8. Étant donné que vous avez sélectionné l’option **Contrôler l’accès** sur la page précédente, la page **Contrôle d’accès** s’affiche à présent. Cette page vous permet de configurer la façon dont l’étiquette applique le chiffrement. Vous pouvez choisir de :  <br/>

    - **Supprimer les paramètres de contrôle d’accès s’ils sont déjà appliqués aux éléments :** lorsque vous sélectionnez cette option, l’application de l’étiquette supprime le chiffrement existant, même s’il a été appliqué indépendamment d’une étiquette de confidentialité. Il est important de comprendre que ce paramètre peut engendrer une étiquette de confidentialité que les utilisateurs peuvent ne pas être en mesure d’appliquer lorsqu’ils ne disposent pas de suffisamment d’autorisations pour supprimer le chiffrement existant.  
    - **Configurer les paramètres de contrôle d’accès :** cette option active le chiffrement avec la gestion des droits. Elle rend également les paramètres suivants visibles : <br/>
        - Attribuer des autorisations maintenant ou laisser les utilisateurs décider ?
        - L’accès des utilisateurs au contenu expire
        - Autoriser l’accès hors connexion

    **Note :** il s’agit d’une stratégie de déploiement courante pour configurer des étiquettes de confidentialité pour initialement ne pas appliquer de chiffrement, puis modifier ultérieurement certaines des étiquettes existantes pour appliquer un chiffrement. C’est l’approche qu’Holly veut suivre. <br/>

    Par conséquent, sélectionnez l’option **Supprimer les paramètres de contrôle d’accès s’ils sont déjà appliqués aux éléments**, puis cliquez sur **Suivant**.

9. Étant donné que vous avez sélectionné l’option **Appliquer le marquage de contenu** sur la page précédente, la page **Marquage de contenu** s’affiche à présent. Définissez le bouton **Marquage de contenu** sur **Activé**. Cela affiche trois options qui vous permettent de personnaliser la façon dont vous souhaitez marquer les fichiers et les e-mails. <br/>

    Cochez les trois cases. Sous chaque paramètre, sélectionnez **Personnaliser le texte**. Cela ouvre un volet permettant de personnaliser le paramètre en question. Entrez les informations suivantes dans le volet **Personnaliser** pour chaque option (sélectionnez **Enregistrer** après avoir entré les paramètres de chaque option) : <br/>

    - **Ajouter un filigrane** 
        - Texte de filigrane : **Sensible – Ne pas partager** (Conseil : après avoir entré cette valeur, copiez-la (Ctrl+C) afin de pouvoir la coller (Ctrl+V) dans les deux autres paramètres textuels)
        - Taille de police : **25**
        - Couleur de police : **Bleu**
        - Disposition du texte : **Diagonal**
            
    - **Ajouter un en-tête** 
        - Texte d’en-tête : **Sensible – Ne pas partager**
        - Taille de police : **25**
        - Couleur de police : **Rouge**
        - Aligner le texte : **Centre**
            
    - **Ajouter un pied de page**
        - Texte du pied de page : **Sensible – Ne pas partager**
        - Taille de police : **25**
        - Couleur de police : **Rouge**
        - Aligner le texte : **Centre**

10. Dans la page **Marquage du contenu**, sélectionnez **Suivant**. 

11. Dans la page **Étiquetage automatique des fichiers et des e-mails**, définissez le bouton bascule **Étiquetage automatique des fichiers et des e-mails** sur **Activé**. Cela active une série d’options que vous mettrez à jour lors des étapes suivantes.

12. Sous **Détecter le contenu qui correspond à ces conditions**, sélectionnez **+Ajouter une condition**, puis **Le contenu contient**.

13. Dans la fenêtre **Le contenu contient**, sélectionnez la flèche déroulante **Ajouter**, puis **Types d’informations sensibles**.

14. Dans la fenêtre **Types d’informations sensibles**, placez votre souris à gauche de l’en-tête de colonne **Nom**. Cochez la case qui s’affiche, afin de sélectionner automatiquement tous les types d’informations sensibles. Sélectionnez **Ajouter**, afin d’ajouter tous ces types d’informations sensibles à votre étiquette.

15. Sur la page **Étiquetage automatique des fichiers et des e-mails**, tous les types d’informations sensibles que vous avez sélectionnés s’affichent. Faites défiler jusqu’au bas de la fenêtre et mettez à jour les paramètres suivants :

    - Lorsque le contenu correspond à ces conditions : sélectionnez **Appliquer automatiquement l’étiquette**.

    - Afficher ce message aux utilisateurs lorsque l’étiquette est appliquée : entrez **Du contenu sensible a été détecté et sera chiffré**.
        
16. Cliquez sur **Suivant**.

17. Dans la page **Définir les paramètres de protection pour les groupes et les sites**, laissez les deux cases décochées, puis sélectionnez **Suivant**.

18. Dans la page **Étiquetage automatique des ressources de données schématisées (préversion)**, n’activez pas l’option Étiquetage automatique des ressources de données schématisées (préversion). Cliquez sur **Suivant**. 

19. Dans la page **Vérifier vos paramètres et terminer**, passez en revue les informations que vous avez entrées. Si des paramètres doivent être corrigés, sélectionnez l’option **Modifier** correspondante et apportez les modifications nécessaires. Lorsque toutes les informations affichées sont correctes, sélectionnez **Créer une étiquette**.

20. Une boîte de dialogue **Erreur du client** doit apparaître, indiquant que l’objet blob de règle généré pour l’étiquette que vous tentez de créer est trop long. La taille maximale des sélections de types d’informations sensibles que vous pouvez effectuer pour chaque règle est **49 152**. En sélectionnant tous les types d’informations sensibles comme vous l’avez fait dans la fenêtre **Types d’informations sensibles**, vous avez dépassé cette limite. <br/>

    **REMARQUE : Nous avons sélectionné délibérément tous les types d’informations sensibles afin que vous receviez cette erreur.** Nous souhaitions que vous rencontriez cette erreur afin que, si elle se produit dans vos environnements de production, vous sachiez pourquoi vous l’avez reçue et comment vous pouvez la corriger.  <br/>

    Pour corriger ce problème, sélectionnez **OK** dans la boîte de dialogue **Erreur du client** puis, dans la page **Vérifier vos paramètres et terminer**, faites défiler jusqu’à **Étiquetage automatique des fichiers et des e-mails** et sélectionnez **Modifier**.
    
21. Cela doit vous renvoyer à la page **Choisir les paramètres de protection pour les éléments étiquetés** de l’Assistant. Sélectionnez **Suivant** dans cette page, sélectionnez **Suivant** dans la page **Chiffrement**, puis sélectionnez **Suivant** dans la page **Marquage du contenu**. Vous accédez alors à la page **Étiquetage automatique des fichiers et des e-mails**. 

22. Dans la page **Étiquetage automatique des fichiers et des e-mails**, à droite de la condition **Le contenu contient**, sélectionnez l’**icône de corbeille**. Cela supprime la condition **Le contenu contient** existante pour l’étiquette **PII** que vous avez créée. <br/>

    Lors des étapes restantes, vous allez ajouter une nouvelle condition qui contient seulement deux types d’informations de confidentialité, plutôt que tous les types d’informations de confidentialité comme initialement.

23. Dans la page **Étiquetage automatique des fichiers et des e-mails**, sous **Détecter le contenu qui correspond à ces conditions**, sélectionnez **+Ajouter une condition**, puis **Le contenu contient**.

24. Dans la fenêtre **Le contenu contient**, sélectionnez la flèche déroulante **Ajouter**, puis **Types d’informations sensibles**.

25. Dans la fenêtre **Types d’informations sensibles**, dans la liste des types d’informations sensibles, cochez uniquement les cases **Numéro de routage ABA** et **Numéro de sécurité sociale (USA)**, puis sélectionnez **Ajouter**. De retour dans la page **Étiquetage automatique des fichiers et des e-mails**, ces deux types d’informations sensibles s’affichent. Cliquez sur **Suivant**.

26. Dans la page **Définir les paramètres de protection pour les groupes et les sites**, laissez les deux cases décochées, puis sélectionnez **Suivant**.

27. Dans la page **Étiquetage automatique des ressources de données schématisées (préversion)**, n’activez pas l’option Étiquetage automatique des colonnes de base de données. Cliquez sur **Suivant**.

28. Dans la page **Vérifier vos paramètres et terminer**, sélectionnez **Créer une étiquette**.

29. Dans la page **Votre étiquette de confidentialité a été créée**, sélectionnez l’option **Ne pas créer de stratégie pour le moment**, puis sélectionnez **Terminé**. Vous revenez alors à la page **Étiquettes**.

30. Il est maintenant temps de publier l’étiquette **PII**. Dans la page **Étiquettes**, si l’étiquette **PII** ne figure pas dans la liste des étiquettes, sélectionnez **Actualiser** dans la barre de menus. Une fois l’étiquette **PII** visible, cochez la case en regard de celle-ci. 

31. Sélectionnez l’option **Publier l’étiquette** qui apparaît dans la barre de menus au-dessus de la liste des étiquettes. Cela lance un Assistant **Création d’une stratégie**.

32. Dans l’Assistant **Création d’une stratégie**, dans la page **Choisir les étiquettes de confidentialité à publier**, l’étiquette **PII** est déjà répertoriée. Sélectionnez **Suivant**. 

33. Dans la page **Affecter des unités d’administration**, sélectionnez **Suivant**, car vous allez affecter cette stratégie d’informations d’identification personnelle à tout l’annuaire d’Adatum plutôt qu’à un groupe spécifique d’unités d’administration.

34. Dans la page **Publier sur des utilisateurs et des groupes**, vous pouvez choisir de rendre votre stratégie disponible pour tous les utilisateurs et groupes, ou la limiter aux utilisateurs et groupes sélectionnés. Pour ce labo, vous souhaitez mettre la stratégie à la disposition de tout le monde. L’option **Utilisateurs et groupes** est déjà sélectionnée par défaut (si ce n’est pas le cas, sélectionnez-la maintenant). Votre stratégie sera alors disponible pour tous les utilisateurs et groupes. Cliquez sur **Suivant**.  <br/>

    **Remarque :** Lorsque vous effectuez cette opération dans votre déploiement réel, si vous souhaitez limiter votre stratégie à certains utilisateurs ou groupes spécifiques, vous devez sélectionner **Modifier** et effectuer ces sélections. 

35. Dans la page **Paramètres de stratégie**, cochez la case **Les utilisateurs doivent fournir une justification pour supprimer une étiquette ou réduire sa classification**, puis sélectionnez **Suivant**. 

36. Dans la page **Appliquer une étiquette par défaut aux documents**, sélectionnez **PII** dans le menu déroulant qui s’affiche, puis **Suivant**.

37. Dans la page **Appliquer une étiquette par défaut aux e-mails**, sélectionnez **PII** dans le menu déroulant qui s’affiche, puis **Suivant**.

38. Dans la page **Appliquer une étiquette par défaut aux réunions et aux événements de calendrier**, sélectionnez **PII** dans le menu déroulant qui s’affiche, puis **Suivant**.

39. Dans la page **Appliquer une étiquette par défaut au contenu Fabric et Power BI**, sélectionnez **PII** dans le menu déroulant qui s’affiche, puis **Suivant**.

40. Dans la page **Nom de votre stratégie**, entrez **Stratégie d’informations d’identification personnelle** dans le champ **Nom**, puis entrez (ou copiez et collez) la description suivante pour cette stratégie d’étiquette de confidentialité : **L’objectif de cette stratégie est de détecter des informations sensibles telles que les numéros de routage de banque ABA et les numéros de sécurité sociale des États-Unis dans les e-mails et les documents, et de chiffrer ces informations lorsqu’elles sont découvertes. L’utilisateur doit fournir une explication pour supprimer l’étiquette de classification.** Cliquez sur **Suivant**.

41. Dans la page **Vérifier, puis terminer**, passez en revue les informations que vous avez entrées. Si quelque chose doit être corrigé, sélectionnez l’option **Modifier**correspondante et apportez les corrections nécessaires. Lorsque toutes les informations sont correctes, sélectionnez **Envoyer**.

42. Dans la page **Nouvelle stratégie créée**, sélectionnez **Terminé**.

43. Laissez votre navigateur Edge ouvert ainsi que tous les onglets. 


### Tâche 4 : affecter une étiquette de confidentialité préexistante à un document

Comme indiqué dans les instructions au début de ce labo, il n’est pas possible de tester immédiatement l’étiquette de confidentialité et la stratégie d’étiquette que vous avez créées lors de la tâche précédente. Cela est dû au fait qu’il faut jusqu’à 24 heures pour qu’une nouvelle stratégie d’étiquette se propage via Microsoft 365 et que son étiquette devienne visible dans les applications telles que Microsoft Word et Outlook.

Au lieu de cela, vous allez tester l’une des étiquettes de confidentialité préexistantes de Microsoft 365. Pour ce labo, vous allez utiliser l’étiquette de sensibilité **Project – Falcon**, qui est une étiquette hautement confidentielle. Cette étiquette est semblable à celle que vous avez créée durant la tâche précédente, la seule exception étant qu’elle n’inclut pas d’en-tête ou de pied de page. L’utilisation de cette étiquette préexistante vous donnera une bonne idée de la façon dont l’étiquette que vous avez créée fonctionnerait chez Adatum.

1. Sur LON-CL1, dans votre navigateur Edge, vous devez toujours être connecté à Microsoft 365 en tant que **Holly Dickson**.

2. Vous allez d’abord passer en revue l’étiquette de confidentialité **Project-Falcon** que vous allez appliquer à un document dans cette tâche.  Dans votre navigateur Edge, vous devez toujours avoir un onglet ouvert pour le portail **Microsoft Purview** de la tâche précédente. Dans le portail **Microsoft Purview**, sous le groupe **Protection des informations** dans le volet de navigation, sélectionnez **Étiquettes**. 

3. Sur la page **Étiquettes**, dans la liste des étiquettes, sélectionnez la flèche droite (**>**) à côté de **Hautement confidentiel** pour afficher les sous-étiquettes sous cette étiquette. Cela affiche l’étiquette préexistante **Project - Falcon**.

4. Sélectionnez l’étiquette **Project - Falcon** (et non la case à cocher ; sélectionnez le nom de l’étiquette). Cela ouvre un volet d'informations **Project - Falcon**. Passez en revue les informations définies pour cette étiquette, puis fermez le volet lorsque vous avez terminé.  

5. Vous allez maintenant attribuer l’étiquette de confidentialité **Project-Falcon** à un document. Sélectionnez l’onglet **Accueil | Microsoft 365** dans votre navigateur pour revenir à la page d’accueil de Microsoft 365. Sélectionnez l’icône **Applications** sur le côté gauche de l’écran. Dans la page **Applications** qui s’affiche, cliquez avec le bouton droit sur la vignette **Word**, puis sélectionnez **Ouvrir dans un nouvel onglet**. 

6. Sous l’onglet **Word | Microsoft 365**, dans la section **Créer nouveau** en haut de la page, sélectionnez **Document vide**.

7. Si une fenêtre **Votre option de confidentialité** s’affiche, sélectionnez **Fermer**.

8. Si le ruban Word affiche des icônes pour chaque fonctionnalité mais ne répartit pas les icônes par groupe, sélectionnez la flèche vers le bas sur le côté droit du ruban puis, sous **Disposition du ruban**, sélectionnez **Ruban Classique**. Cela permet de basculer vers le style de ruban traditionnel, qui affiche une répartition par groupe de fonctionnalités (par exemple, Annuler, Presse-papiers, Police, Paragraphe, Styles, et ainsi de suite).

9. Dans le document **Word**, tapez le texte suivant : **Test d’une étiquette de confidentialité sur un document avec des informations d’identification personnelle, en l’occurrence un numéro de sécurité sociale des USA : 111-11-1111.**

10. Étant donné que vous avez activé les étiquettes de confidentialité au début de cet exercice, **Word** doit afficher un groupe **Confidentialité** sur le ruban en haut de la page. Sélectionnez la flèche vers le bas dans le groupe **Confidentialité**. Dans le menu déroulant qui s’affiche doit figurer la liste des types d’étiquettes de confidentialité. Sélectionnez **Hautement confidentiel** puis, dans le sous-menu qui s’affiche, sélectionnez **Project – Falcon**. <br/>

    **Remarque :** Après 24 heures, l’étiquette que vous avez créée durant la tâche précédente apparaîtra dans le sous-menu Hautement confidentiel, à côté de l’étiquette Project - Falcon. Mais pour l’heure, vous allez utiliser l’étiquette **Project – Falcon** à la place.

11. Dans le document, notez que l’étiquette a appliqué un filigrane **CONFIDENTIEL – ProjectFalcon** en haut du document. L’étiquette Project – Falcon a été configurée exactement comme celle que vous avez créée, où le filigrane était censé apparaître en diagonale au milieu de la page. Alors pourquoi apparaît-il en haut de la page ? La réponse est que vous utilisez **Word pour le web**, qui par défaut l’affiche comme vous le voyez ici. Pour voir comment il apparaîtra à quelqu’un qui lit le document, vous devez afficher le document en **Mode Lecture**, ce que vous allez faire dès maintenant. <br/>

    Sélectionnez l’onglet **Affichage** puis, dans le ruban Word, sélectionnez **Mode Lecture**. Notez que le filigrane apparaît en diagonale au milieu du document. C’est comme cela qu’il apparaîtra à quelqu’un lisant le document. Notez que si vous utilisez l’application de bureau Word, le filigrane sera affiché tel que désigné par l’étiquette (à savoir, dans le cas présent, exactement comme vous le voyez ici en Mode Lecture). <br/>

    Pour quitter le Mode Lecture, sélectionnez **Modifier le document** dans la barre de menus en haut de la page. Dans le menu déroulant qui apparaît, sélectionnez **Modifier**.

12. Dans ce premier test de validation, vous allez faire en sorte que cette étiquette de confidentialité ne soit pas appliquée à ce document. L’une des options de stratégie d’étiquette exige que les utilisateurs fournissent une justification pour supprimer une étiquette ou sélectionner une étiquette de classification inférieure. Vous allez maintenant vérifier si ce paramètre fonctionne correctement. <br/>

    Dans le groupe **Confidentialité** du ruban Word, sélectionnez la flèche vers le bas. Dans le menu déroulant qui s’affiche, notez qu’une coche apparaît en regard de **Hautement confidentiel**. Maintenez le curseur de la souris sur **Hautement confidentiel** pour afficher le sous-menu. Notez qu’une coche apparaît en regard de **Project – Falcon**. Les coches identifient l’étiquette actuellement appliquée au document.  <br/>
 
    Pour supprimer l’étiquette de ce document, sélectionnez l’étiquette **Project – Falcon** qui apparaît dans ce menu déroulant.
    
13. Dans la fenêtre **Justification requise** qui s’affiche, sélectionnez l’option **Autre (expliquer)**. Dans le champ **Expliquez pourquoi vous modifiez cette étiquette**, entrez **Test de ce qui se produit lorsqu’une étiquette est supprimée d’un document**, puis sélectionnez **Modifier**.

14. Notez que le filigrane dans le document a disparu. Dans le groupe **Confidentialité** du ruban Word, sélectionnez la flèche vers le bas. Dans le menu déroulant qui s’affiche, notez que bien que **Hautement confidentiel** > **Project – Falcon** soit affiché, aucune coche n’est visible en regard. Cela indique que l’étiquette de confidentialité n’est plus appliquée à ce document.  

15. Pour réappliquer l’étiquette de confidentialité au document, sélectionnez **Hautement confidentiel** > **Project – Falcon** dans le menu déroulant. Notez que le filigrane réapparaît dans le document.

16. Vous allez maintenant enregistrer le document afin de pouvoir le partager durant la tâche suivante. Un champ de nom de document qui contient une flèche déroulante s’affiche en haut à gauche de la page, à droite de l’icône Word (Word est susceptible d’afficher **Document** ou **Document1** comme nom de fichier temporaire). Sélectionnez la flèche déroulante. Dans le menu déroulant qui s’affiche, confirmez que l’**Emplacement** du fichier indique **Holly Dickson > Documents**. <br/>

    Dans le champ **Nom du fichier**, renommez le fichier **DocumentProtégé1**, puis cliquez en dehors de ce menu de nom de fichier (cliquez à l’intérieur du document). Notez que le nouveau nom affecté au fichier apparaît dans la barre de titre. 

17. Laissez l’onglet **DocumentProtégé1** ouvert, avec le document affiché. Vous reviendrez à ce document durant la tâche suivante afin de le partager avec Joni Sherman.

Vous venez de créer un document Word contenant l’étiquette Hautement confidentielle intitulée **Project – Falcon**. 


### Tâche 5 : protéger un document en utilisant Protection des données Microsoft Purview

Durant la tâche précédente, vous avez créé un document Word et vous l’avez protégé avec l’étiquette de confidentialité **Project – Falcon**. Cette étiquette a inséré un filigrane dans le document. Lors de cette tâche, vous allez partager le document que vous avez créé avec Joni Sherman, et restreindre Joni à l’autorisation « Affichage uniquement ». Cela vous permettra de voir comment Protection des données Microsoft Purview protège le document en fonction des paramètres que vous configurez.

Pour vérifier si la protection que vous avez affectée au document fonctionne, vous devez d’abord envoyer le document par e-mail à deux personnes : à Joni Sherman et à votre propre adresse e-mail personnelle. Vous vérifierez ensuite que Joni peut uniquement afficher le document (et pas le modifier), et vous vérifierez que vous ne pouvez pas accéder au document, car il n’a pas été partagé avec vous. Pour finir, vous modifierez l’autorisation sur le document afin que Joni puisse le modifier, et vous lui enverrez ce document mis à jour par e-mail à des fins de test. L’objectif des deux e-mails à Joni, l’un avec un lien de document qui fournit un accès en lecture seule et l’autre avec un lien de document qui autorise sa modification, est de voir comment Microsoft Entra ID Protection peut fournir différents niveaux de protection des documents. 

1. Sur LON-CL1, dans votre navigateur Edge, vous devez toujours être connecté à Microsoft 365 en tant que **Holly Dickson** (suite à la tâche précédente) avec l’onglet **Word** ouvert.

2. Dans votre navigateur Edge, sélectionnez l’onglet **Applications | Microsoft 365**. 

3. Dans la page **Applications**, cliquez avec le bouton droit sur la vignette **Outlook** et sélectionnez **Ouvrir dans un nouvel onglet**. La boîte aux lettres d’Holly s’ouvre dans Outlook sur le web dans un nouvel onglet de navigateur. 

4. Dans **Outlook sur le web**, sélectionnez **Nouveau courrier** en haut de l’écran.

5. Entrez les informations suivantes dans le formulaire d’e-mail :

    - Par : entrez **Joni**, puis sélectionnez **Joni Sherman** dans la liste des utilisateurs. 

    - CC : entrez votre propre adresse e-mail personnelle (n’entrez PAS l’adresse e-mail d’Holly ; entrez plutôt votre propre adresse e-mail personnelle), puis sélectionnez le message **Utiliser cette adresse : <your email address>** qui s’affiche.

    - Ajoutez un objet : **Test de document protégé – Autorisation Affichage uniquement**

    - Corps du message : entrez **Ouvrez le document protégé joint à cet e-mail et essayez de le modifier.**

6. Dans le corps du message, sous le texte que vous avez ajouté à l’étape précédente, vous joindrez un lien au document que vous avez créé durant la tâche précédente. Toutefois, pour ce faire, vous devez d’abord partager le document avec Joni Sherman, en appliquant des autorisations restreintes **Affichage uniquement**. Pour cela, vous devez quitter cet e-mail, revenir à votre document et le partager avec Joni. Une fois que vous aurez copié le lien créé pendant le processus de partage, vous reviendrez à cet e-mail et collerez le lien. <br/>

    Dans votre navigateur Edge, sélectionnez l’onglet **DocumentProtégé1**, qui doit toujours afficher le document que vous avez créé durant la tâche précédente. En haut à droite de la page, sous le nom et les initiales d’Holly Dickson, sélectionnez le bouton **Partager**. Dans le menu déroulant qui s’affiche, sélectionnez **Partager**.

7. Dans la fenêtre **Partager « DocumentProtégé1 »** qui s’affiche, sélectionnez l’icône d’engrenage (**Paramètres du lien**) qui apparaît en regard du bouton **Copier le lien**. 

8. Dans la fenêtre **Paramètres du lien** qui s’affiche, sélectionnez l’option **Contacts que vous choisissez**.
    
9. Sous **Plus de paramètres**, l’option actuelle est **Modification**. Vous prévoyez de partager ce document avec Joni Sherman, mais vous souhaitez qu’elle puisse uniquement l’afficher. Pour modifier ces autorisations, sélectionnez **Modification**. Dans le menu qui s’affiche, passez en revue les options disponibles. Vous pouvez voir que l’option **Modification** est cochée, ce qui indique qu’il s’agit du paramètre actuel. Pour limiter Joni à l’autorisation Lecture seule, sélectionnez **Afficher**, puis **Appliquer**.

10. Vous revenez alors à la fenêtre **Partager « DocumentProtégé1 »**. Entrez **Joni** dans le champ **Ajouter un nom, un groupe ou un e-mail**. Une liste d’utilisateurs dont le nom commence par **Joni** doit apparaître. Sélectionnez **Joni Sherman**.

11. Dans la fenêtre **Partager « DocumentProtégé1 »**, pointez votre souris sur l’icône « œil » qui apparaît à droite du nom de Joni. La mention **Afficher**, qui est le paramètre actuel que vous lui avez affecté pour ce document, doit alors apparaître. L’icône « œil » est synonyme d’autorisation « Afficher ». Sélectionnez le bouton **Copier le lien**. 

12. Une fois que le message **Lien copié** apparaît en bas de la fenêtre **Partager "ProtectedDocument1"**, sélectionnez le X dans le coin supérieur de la fenêtre pour la fermer.

13. Dans votre navigateur Edge, sélectionnez l’onglet **Courrier – Holly Dickson – Outlook** pour revenir à votre e-mail. Dans le corps du message, sous le texte que vous avez ajouté précédemment, collez (Ctrl+V) le lien vers le document partagé que vous venez de copier dans le Presse-papiers. Un lien pour le fichier nommé **DocumentProtégé1.docx** doit apparaître. 

14. Sélectionnez **Envoyer**.

15. Un message **Les destinataires ne peuvent pas accéder aux liens** doit s’afficher. Ce message indique que Microsoft Entra ID Protection reconnaît le fait que vous avez inclus dans l’e-mail votre adresse e-mail personnelle, qui n’a pas l’autorisation d’accéder au document. Pour les besoins de ce test de labo, sélectionnez **Envoyer quand même**.

16. Basculez vers **LON-CL2**. 

17. Sur **LON-CL2**, vous devez être connecté à **Outlook sur le web** en tant que **Lynne Robbins** suite à l’exercice de labo précédent. Déconnectez-vous en tant que Lynne.

18. Dans votre navigateur Edge, fermez tous les onglets sauf **Se déconnecter**. Sous cet onglet, entrez l’URL suivante dans la barre d’adresse : **https://outlook.office365.com** 

19. Dans la fenêtre **Choisir un compte**, sélectionnez **Utiliser un autre compte**.

20. Dans la fenêtre **Se connecter**, entrez **JoniS@xxxxxZZZZZZ.onmicrosoft** (où xxxxxZZZZZZ est le préfixe de locataire fourni par votre fournisseur d’hébergement de labo), puis sélectionnez **Suivant**.

21. Dans la fenêtre **Entrer le mot de passe**, entrez le nouveau mot de passe de l’utilisateur que vous avez précédemment affecté au compte de Joni, puis sélectionnez **Se connecter**. 

22. Si une fenêtre **Bienvenue** s’affiche, sélectionnez le X pour la fermer.

23. Dans la **Boîte de réception** de Joni dans **Outlook sur le web**, vous devez voir l’e-mail que Holly vient d’envoyer, dont la ligne Objet indique que le document dispose d’une autorisation Affichage uniquement. Ouvrez cet e-mail.

24. Dans l’e-mail, sélectionnez le fichier joint pour l’ouvrir.

25. Dans la fenêtre **Votre option de confidentialité** qui s’affiche, sélectionnez **Fermer**. Le document s’ouvre dans **Word sur le web** dans un nouvel onglet de navigateur intitulé **DocumentProtégé1.docx**. Notez que le document s’affiche en Mode Lecture dans **Word sur le web**. Cela indique à Joni qu’elle dispose de l’autorisation Affichage uniquement, et qu’elle ne peut pas modifier le document. Pour vérifier cela, essayez de sélectionner à l’intérieur du document. Notez le message qui s’affiche : **Lecture seule. Ce document est en lecture seule.** Notez le filigrane spécifié dans la stratégie **Project – Falcon**. <br/>

    Une fois que vous avez terminé de passer en revue le document, fermez l’onglet **DocumentProtégé1.docx**. 

26. Vous allez maintenant tester ce qui se produit lorsque vous tentez d’ouvrir le document envoyé à votre adresse e-mail personnelle. Utilisez votre téléphone mobile ou votre PC de classe pour accéder à votre boîte aux lettres personnelle. Ouvrez l’e-mail que Holly vient d’envoyer à votre adresse e-mail personnelle, puis essayez d’ouvrir le fichier joint. 

27. Étant donné que vous n’êtes pas autorisé à accéder au document, une fenêtre **Choisir un compte** doit apparaître. Dans un scénario réel, vous pourriez éventuellement vous connecter avec un compte autorisé à accéder au fichier, ou demander l’accès à partir du compte **Holly@xxxxxZZZZZZ.onmicrosoft.com**. <br/>

    Dans le cadre de ce test, vous venez de vérifier que vous ne pouvez pas accéder au fichier, car il n’a pas été partagé avec vous. Vous avez également vérifié que Joni était uniquement en mesure d’afficher le fichier, mais pas de le modifier. Vous allez maintenant modifier les autorisations de partage sur le fichier en autorisant Joni à le modifier, afin de voir comment cette expérience diffère de celle que vous venez de terminer. 

28. Basculez vers **LON-CL1**. 

29. Sur LON-CL1, dans votre navigateur Edge, vous devez toujours être connecté à Microsoft 365 en tant que **Holly Dickson**, et vous devez avoir des onglets ouverts pour **Word** et **Outlook**. Sélectionnez l’onglet **Courrier – Holly Dickson – Outlook**. 

30. Dans la boîte aux lettres d’Holly, créez un autre e-mail destiné à Joni Sherman. N’incluez PAS votre adresse e-mail personnelle sur la ligne CC. Entrez les informations suivantes dans le formulaire d’e-mail :

    - Par : entrez **Joni**, puis sélectionnez **Joni Sherman** dans la liste des utilisateurs. 

    - CC : laissez cette ligne vide.

    - Ajoutez un objet : **Test de document protégé – Autorisation Modifier**

    - Corps du message : entrez **Ouvrez le document protégé joint à cet e-mail et essayez de le modifier.**

31. Tout comme avec l’e-mail précédent, vous devez maintenant partager le document avec Joni, mais cette fois avec l’autorisation Modifier. Pour ce faire, procédez comme suit : <br/>

    - Sélectionnez l’onglet **DocumentProtégé1** dans votre navigateur puis, sur le côté droit de la barre de menus, sélectionnez le bouton **Partager**. Dans le menu déroulant qui s’affiche, sélectionnez **Partager**. 
    - Dans la fenêtre **Partager « DocumentProtégé1 »**, entrez **Joni** dans le champ **Ajouter un nom, un groupe ou un e-mail**, puis sélectionnez **Joni Sherman**.
    - À droite du nom de Joni figure une icône de crayon (**Modification**). Il s’agit de l’autorisation par défaut lors du partage d’un document. Sélectionnez le bouton **Copier le lien** pour voir ce qui se passe.
    - Notez le message **Lien copié** qui s’affiche. Ce message indique que tout le monde peut modifier le document, bien que vous ayez spécifié le nom de Joni. Ce n’est pas ce que vous voulez, car vous souhaitez faire en sorte que Joni soit la seule personne à pouvoir le modifier. Pour mettre cette restriction en place, sélectionnez l’icône d’engrenage (**Paramètres du lien**) en regard du bouton **Copier le lien**. 
    - Dans la fenêtre **Paramètres du lien** qui s’affiche, sélectionnez l’option **Contacts que vous choisissez**. Cette option est la clé pour limiter l’autorisation aux utilisateurs sélectionnés. 
    - Sous **Plus de paramètres**, si **Modification** est visible, sélectionnez **Appliquer**. Toutefois, si **Afficher** est visible, sélectionnez **Afficher** puis, dans le menu qui s’affiche, sélectionnez **Modification**, puis **Appliquer**. 
    - Dans la fenêtre **Partager « DocumentProtégé1 »**, sélectionnez le bouton **Copier le lien**.
    - Notez le message **Lien copié** qui s’affiche. Cette fois, le message indique que seules les personnes que vous spécifiez peuvent modifier le document. Dans ce cas, la modification sera limitée à Joni, car vous n’avez spécifié qu’elle. 
    - Sélectionnez l’onglet **Courrier – Holly Dickson – Outlook** dans votre navigateur, puis collez le lien dans le corps de l’e-mail. 

32. Sélectionnez **Envoyer**.

33. Basculez vers **LON-CL2**. 

34. Sur **LON-CL2**, vous devez toujours être connecté à **Outlook sur le web** en tant que **Joni Sherman**. Dans la **Boîte de réception** de Joni, vous devez voir l’e-mail que Holly vient d’envoyer, dont la ligne Objet indique que le document dispose d’une autorisation Modifier. Ouvrez cet e-mail.

35. Dans l’e-mail, sélectionnez le fichier joint pour l’ouvrir.

36. Lorsque Joni avait l’autorisation Affichage uniquement, le document s’ouvrait dans le volet Mode Lecture. Par conséquent, Joni ne pouvait pas le modifier. Cette version du document fournit à Joni l’autorisation Modifier. Cette fois, le document doit donc s’ouvrir dans Word en mode d’édition normal. Vérifiez que vous pouvez entrer du texte dans le document. 

    **Remarque :**  Dans cette tâche, vous avez vérifié que Protection des données Microsoft Purview protégeait le document en fonction des paramètres de stratégie des informations d'identification personnelle que vous avez configurés. Lorsque Joni disposait de l’autorisation Affichage uniquement, le document s’ouvrait en Mode Lecture et elle ne pouvait pas le modifier. Lorsque l’autorisation Modifier a été octroyée à Joni, le document s’est ouvert dans Word et elle a pu le modifier. Et comme Holly n’a pas partagé le document avec vous, vous n’avez pas pu l’ouvrir quand elle l’a envoyé dans un e-mail à votre boîte aux lettres personnelle. 

## Fin du labo 4


# Félicitations ! Vous venez de terminer le dernier labo de ce cours.
