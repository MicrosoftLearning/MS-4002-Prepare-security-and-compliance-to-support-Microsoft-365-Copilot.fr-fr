# Parcours d’apprentissage 1 - Labo 3 - Exercice 1 - Gérer des stratégies DLP  

Jouant le rôle d’Holly Dickson, la nouvelle administratrice Microsoft 365 d’Adatum, vous avez déployé Microsoft 365 dans un environnement de laboratoire virtualisé. Pour les étapes suivantes de votre travail sur votre projet pilote Microsoft 365, vous allez implémenter des stratégies de protection contre la perte de données (DLP) à Adatum. Vous allez commencer par créer une stratégie DLP personnalisée dans cet exercice, puis vous allez tester les stratégies DLP liées à l’archivage d’e-mails et aux e-mails contenant des données sensibles. 

### Tâche 1 - Créer une stratégie DLP avec des paramètres personnalisés

Dans cet exercice, vous allez créer une stratégie de protection contre la perte de données dans le portail Microsoft Purview pour protéger les données sensibles contre le partage par les utilisateurs. La stratégie DLP que vous créez va informer vos utilisateurs s’ils souhaitent partager du contenu contenant des adresses IP. 

La stratégie contient deux règles, ou actions, dont chacune dépend du nombre d’adresses IP dans le message. Si le message contient une adresse IP, la stratégie avertit les personnes à l’aide d’un conseil de stratégie et envoie l’e-mail. Toutefois, si le contenu contient deux adresses IP ou plus, le message est alors bloqué, un e-mail d’incident avec un niveau de confidentialité élevé est envoyé à l’expéditeur et un conseil de stratégie s’affiche, qui permet à l’expéditeur d’ignorer le blocage de l’e-mail si l’expéditeur fournit une justification professionnelle dans le conseil de stratégie.

1. Sur LON-CL1, dans votre navigateur Edge, vous devez toujours être connecté à Microsoft 365 en tant que **Holly Dickson**. 

2. Dans **Microsoft Edge**, le portail Microsoft Purview devrait encore être ouvert. Sinon, ouvrez un nouvel onglet et accédez à **https://compliance.microsoft.com**.

3. Dans le **portail Microsoft Purview**, dans le volet de navigation, sélectionnez **Solutions**, **Protection contre la perte de données**, puis **Stratégies**.

4. Sur la page **Stratégies**, sélectionnez l’option **+Créer une stratégie** dans la barre de menu pour démarrer l’assistant **Créer une stratégie**.

5. Dans le menu **Démarrer avec un modèle ou créer une page de stratégie personnalisée**, la colonne **Catégories** affiche les catégories de stratégie. Chaque catégorie de stratégie fournit des modèles qui peuvent être utilisés pour créer ce type de stratégie, à l’exception de la catégorie **Personnalisée**. Cette catégorie ne fournit aucun modèle spécifique. Au lieu de cela, elle permet aux organisations de créer des stratégies personnalisées à partir de zéro. Lorsque vous sélectionnez une catégorie, la colonne **Modèles** apparaît et affiche les modèles disponibles parmi lesquels il est possible de choisir pour la catégorie sélectionnée. Lorsque vous sélectionnez un modèle, une autre colonne apparaît, qui affiche le type d’informations protégées dans ce modèle. <br/> 

    Par exemple, sélectionnez **Financier** dans le volet latéral, puis faites défiler les différents modèles que vous pouvez choisir dans la colonne **Modèles**. Sélectionnez un ou deux des modèles pour voir le type d’informations que ceux-ci protègent. Si vous le souhaitez, sélectionnez chacune des catégories restantes pour voir quel type de modèles sont fournis. 
  
6. Dans le cadre de ce labo, vous allez créer une stratégie DLP personnalisée. Sélectionnez **Personnalisée** dans la colonne **Catégories**, puis sélectionnez le modèle **Stratégie personnalisée** dans la colonne **Modèles**, et cliquez sur **Suivant**.

7. Sur la page **Nommer votre stratégie DLP**, entrez les informations suivantes, puis sélectionnez **Suivant** :  <br/>

      - Nom : **Stratégie DLP d’adresse IP**
      - Description : **Cette stratégie détecte la présence d’adresses IP dans les e-mails. Les utilisateurs finaux sont avertis de la détection et les administrateurs reçoivent une notification. Les e-mails contenant 2 adresses IP ou plus sont bloqués.**

8. Sur la page **Affecter des unités d’administration**, sélectionnez **Suivant**. 

9. Sur la page **Choisir où affecter la stratégie**, vérifiez que le bouton **État** est défini sur **activé** pour les emplacements suivants (si l’un de ces emplacements n’est pas défini sur **Activé** par défaut, définissez-le immédiatement sur **Activé**) : <br/>

    - **Messagerie Exchange**
    - **Sites SharePoint**
    - **Comptes OneDrive**
    - **Conversations et messages de canaux Teams**

    Définissez tous les autres emplacements sur **Désactivé**, puis sélectionnez **Suivant**.

10. Sur la page **Définir les paramètres de stratégie**, l’option **Créer ou personnaliser des règles DLP avancées** doit être activée par défaut (si elle n’est pas déjà sélectionnée par défaut, alors sélectionnez-la), puis sélectionnez **Suivant**. 

11. Sur la page **Personnaliser les règles DLP avancées**, sélectionnez l’option **+ Créer une règle** dans la barre de menu.

12. Sur la page **Créer une règle**, entrez les informations suivantes :
    
      - Nom : **Règle d’adresse IP unique**
    
      - Description : **L’e-mail contient une adresse IP**
    
      - Dans la section **Conditions**, sélectionnez **+ Ajouter une condition**, puis **Le contenu contient** dans le menu déroulant qui s’affiche. Saisissez ensuite les paramètres de condition suivants :
    
        - Dans le champ **Le contenu contient**, sélectionnez le menu déroulant **Ajouter**, puis **Types d’informations sensibles**.
        
        - Dans le volet **Types d’informations sensibles**, saisissez **IP** dans le champ **Recherche**, puis appuyez sur Entrée.
        
        - Dans les résultats de recherche, cochez la case **Adresse IP**, puis sélectionnez **Ajouter**.
        
     - Faites défiler jusqu’à la section **Notifications utilisateur**, puis définissez le bouton **Utiliser les notifications pour informer vos utilisateurs et les aider à comprendre comment utiliser correctement des informations sensibles** sur **Activé**.

    - Cochez la case **Informer les utilisateurs dans le service Office 365 avec un conseil de stratégie**. Dans la section **Conseils de stratégie**, cochez la case **Personnaliser le texte du conseil de stratégie**. 

        - Holly souhaite que vous personnalisiez le message du conseil de stratégie. Saisissez donc le texte suivant dans ce champ : **ATTENTION ! Vous avez saisi des informations sensibles (une adresse IP) dans ce message. Cela ne vous empêchera pas d’envoyer ce message, mais vous devriez vérifiez si les destinataires sont autorisés à voir ces données sensibles.** 

    - Cochez la case **Afficher le conseil de stratégie sous forme de boîte de dialogue pour l’utilisateur final avant l’envoi (disponible pour la charge de travail Exchange uniquement).** 
    
    - Dans la section **Rapports d’incidents**, vérifiez que l’option **Envoyer une alerte aux administrateurs lorsqu’une correspondance de règle se produit** est définie sur **Activé** (si nécessaire, définissez-la sur **Activé**).

    - Sélectionnez au bas de la page le bouton **Enregistrer**.

13. Sur la page **Personnaliser les règles DLP avancées**, la **règle d’adresse IP unique** que vous venez de créer doit maintenant apparaître. Sélectionnez l’option **+ Créer une règle** pour créer la deuxième règle DLP. 

14. Sur la page **Créer une règle**, entrez les informations suivantes :
    
    - Nom : **règle d’adresses IP multiples**
    
    - Description : **L’e-mail contient deux adresses IP ou plus**
    
    - Dans la section **Conditions**, sélectionnez **+ Ajouter une condition**, puis **Le contenu contient** dans le menu déroulant qui s’affiche. Saisissez ensuite les paramètres de condition suivants :
    
        - Dans le champ **Le contenu contient**, sélectionnez le menu déroulant **Ajouter**, puis **Types d’informations sensibles**.
        
        - Dans le volet **Types d’informations sensibles**, saisissez **IP** dans le champ **Recherche**, puis appuyez sur Entrée.
        
        - Cochez la case **Adresse IP**, puis sélectionnez **Ajouter**.

        - Dans la section **Types d’informations sensibles**, le type d’informations **Adresse IP** s’affiche. À droite de la ligne Adresse IP, le paramètre **Nombre d’instances** est défini de **1** à **Toutes**. Remplacez la valeur 1 du premier champ par **2**. Avec cette modification, cette règle s’appliquera uniquement si 2 adresses IP ou plus apparaissent dans l’e-mail. 
    
    - Dans la section **Actions**, sélectionnez **+ Ajouter une action**. Dans le menu déroulant qui s’affiche, sélectionnez **Restreindre l’accès ou chiffrer le contenu dans les emplacements Microsoft 365**. Entrez ensuite les paramètres d’action suivants :

    - Si aucune option n’apparaît dans la section **Restreindre l’accès ou chiffrer le contenu dans les emplacements Microsoft 365**, sélectionnez-la pour la développer. Cette section doit afficher l’option **Empêcher les utilisateurs de recevoir des e-mails ou d’accéder à des fichiers partagés à partir de SharePoint, OneDrive et Teams**, qui est sélectionnée par défaut. Laissez cette option non sélectionnée.

    - Sous l’option **Empêcher les utilisateurs de recevoir des e-mails ou d’accéder à des fichiers partagés à partir de SharePoint, OneDrive et Teams**, sélectionnez l’option **Bloquer tout le monde**.
    
    - Dans la section **Notifications utilisateur**, définissez l’option **Utiliser des notifications pour informer vos utilisateurs et les aider à comprendre comment utiliser correctement des informations sensibles**, sur **Activé**. 

    - Cochez la case **Informer les utilisateurs dans le service Office 365 avec un conseil de stratégie**. Dans la section **Conseils de stratégie**, cochez la case **Personnaliser le texte du conseil de stratégie**. 

        - Holly souhaite que vous personnalisiez le message du conseil de stratégie. Saisissez donc le texte suivant dans ce champ : **ATTENTION ! Vous avez entré des informations sensibles (plusieurs adresses IP) dans ce message. Vous serez bloqué si vous tentez d’envoyer ce message. Si vous ignorez ce blocage, cela signifie que autorisez l’envoi de ces données sensibles aux destinataires.** 

    - Cochez la case **Afficher le conseil de stratégie sous forme de boîte de dialogue pour l’utilisateur final avant l’envoi (disponible pour la charge de travail Exchange uniquement).** 
    
    - Dans la section **Contournements utilisateur**, cochez la case **Autoriser les contournements à partir de fichiers Microsoft 365 et d’éléments Microsoft Fabric**. Cela active des paramètres supplémentaires qui indiquent comment les contournements seront gérés. Cochez chaque case pour les deux options suivantes :

        - **Exiger une justification professionnelle pour contourner**
        - **Ignorer automatiquement la règle si elle est signalée comme faux positif**
    
    - Dans la section **Rapports d’incidents**, vérifiez que l’option **Envoyer une alerte aux administrateurs lorsqu’une correspondance de règle se produit** est définie sur **Activé** (si nécessaire, définissez-la sur **Activé**).

    - Sélectionnez au bas de la page le bouton **Enregistrer**.

15. Sur la page **Personnaliser les règles DLP avancées**, la **règle d’adresse IP unique** et la **règle d’adresses IP multiples** doivent maintenant apparaître toutes les deux. Cliquez sur **Suivant**.

16. Sur la page **Mode de stratégie**, sélectionnez **Activer immédiatement la stratégie**, puis **Suivant**.

17. Sur la page **Vérifier et terminer**, vérifiez la stratégie que vous venez de créer. Si quelque chose doit être corrigé, sélectionnez l’option **Modifier** correspondante et apportez les corrections nécessaires. Lorsque tout vous semble correct, cliquez sur **Envoyer**.

18. L’affichage de la page **Nouvelle stratégie créée** peut prendre environ une minute. Lorsque celle-ci s’affiche, sélectionnez **Terminé**.

19. Laissez votre navigateur Edge ouvert. Ne fermez aucun des onglets.


Vous avez maintenant créé une stratégie DLP qui analyse les adresses IP dans les e-mails et dans les documents envoyés ou partagés au sein de votre organisation.


### Tâche 2 - Désactiver la fonctionnalité Envoyer à Kindle qui contourne les stratégies DLP

Holly Dickson, administratrice Microsoft 365 d’Adatum, a récemment découvert la fonctionnalité **Envoyer à Kindle** dans Microsoft 365 qui permet d’envoyer des documents Microsoft Word directement vers votre bibliothèque Kindle en quelques minutes. Un fichier transféré peut apparaître comme un livre Kindle avec des tailles de police réglables ou comme un document imprimé avec des dispositions fixes afin de préserver votre mise en page. 

Le problème de cette fonctionnalité est que les stratégies DLP ne prennent pas en compte le partage de fichiers Word vers Kindle, ce qui a pour effet de contourner les contrôles DLP. Étant donné qu’Adatum n’utilise pas la fonctionnalité **Envoyer à Kindle**, Holly souhaite la désactiver pour éviter toute situation permettant à des utilisateurs de contourner les stratégies DLP de l’entreprise. 

Pour désactiver ce paramètre, vous devez créer une stratégie pour les application Office dans le Centre d’administration Microsoft Intune. Dans la stratégie que vous créez, vous allez ajouter le paramètre **Désactiver Envoyer vers Kindle** à la stratégie, puis activer ce paramètre. L’activation de ce paramètre dans la stratégie désactive la fonctionnalité **Envoyer vers Kindle** une fois que vous avez terminé de créer la stratégie. À partir de ce moment, les utilisateurs ne pourront plus envoyer de documents Word vers leur bibliothèque Kindle.

**Note :** ce problème est quelque chose que vous devez prendre en compte dans vos déploiements Microsoft 365 réels. Pour plus d’informations sur la fonctionnalité **Envoyer vers Kindle**, consultez https://support.microsoft.com/office/send-to-kindle-a53d880d-9952-4bf1-abc5-6bce8db5a273.

1. Sur LON-CL1, dans votre navigateur Edge, vous devez toujours être connecté à Microsoft 365 en tant que **Holly Dickson**. 

2. Dans votre navigateur Edge, accédez à l’onglet **Centre d’administration Microsoft 365**. Dans le volet de navigation du centre d’administration Microsoft 365, dans le groupe **Centres d’administration**, sélectionnez **Endpoint Manager**.

3. Dans le **centre d’administration Microsoft Intune** qui s’ouvre dans un nouvel onglet, dans le volet de navigation, sélectionnez **Applications**.

4. Sur la page **Applications | Vue d’ensemble**, dans le volet de navigation du milieu, sélectionnez **Stratégies pour applications Office** dans la **section Stratégie**.

5. Sur la page **Applications | Stratégies pour applications Office**, sélectionnez le **bouton Créer**. Cela lance un assistant pour créer une nouvelle stratégie. Lors des étapes suivantes, vous allez activer le paramètre **Désactiver l’envoi vers Kindle** dans cette stratégie.

6. Sur la page **Démarrer avec les principes de base**, saisissez **Désactiver le paramètre Envoyer vers Kindle** dans le **champ Nom**, puis sélectionnez **Suivant**.

7. Sur la page **Choisir l’étendue**, sélectionnez l’option **Cette configuration de stratégie s’applique à tous les utilisateurs**, puis sélectionnez **Suivant**.

8. Sur la page **Configurer les paramètres**, observez les mesures affichées au-dessus de la liste des paramètres. Il existe plus de 2200 paramètres d’applications Office pour la configuration de votre locataire. Pour localiser rapidement ce paramètre, saisissez **Kindle** dans le champ **Recherche**, puis appuyez sur **Entrée**. Cela doit afficher toutes les stratégies comportant **Kindle** dans le nom de la stratégie.

9. Comme vous pouvez le constater, il n’y a qu’un seul paramètre Kindle, qui est **Désactiver Envoyer vers Kindle**. Sélectionnez ce paramètre, qui ouvre le volet **Désactiver Envoyer vers Kindle**.

10. Dans le volet **Désactiver Envoyer vers Kindle**, les plateformes et les applications auxquelles ce paramètre s’applique s’affichent. Sous la description, sélectionnez l’option **Afficher plus**. Lisez la description complète de ce paramètre.

11. Sélectionnez la flèche déroulante du champ **Paramètre de configuration**. Dans le menu déroulant qui apparaît, sélectionnez **Activé**.

12. Sélectionnez le bouton **Appliquer** en bas du volet.

13. Sur la page **Configurer les paramètres**, la stratégie **Désactiver Envoyer vers Kindle** doit apparaître et son **Statut** doit être **Configuré**. Cliquez sur **Suivant**.

14. Sur la page **Vérifier la configuration et créer**, sélectionnez le bouton **Créer**. 

15. Sur la page **Nouvelle configuration de stratégie créée**, sélectionnez **Terminé**.
 
16. Laissez votre navigateur Edge ouvert. Ne fermez aucun des onglets.


En activant le paramètre **Désactiver Envoyer vers Kindle** dans la nouvelle stratégie que vous venez de créer, vous avez désactivé la fonctionnalité **Envoyer vers Kindle**. Cela va empêcher les utilisateurs Adatum d’envoyer des documents Word vers leur bibliothèque Kindle, action qui contournerait les stratégies DLP de l’entreprise.


# Passez au labo 3 – Exercice 2 
