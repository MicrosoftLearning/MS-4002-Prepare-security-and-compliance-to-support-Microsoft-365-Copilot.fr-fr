# Parcours d’apprentissage 1 - Labo 3 - Exercice 2 - Tester la stratégie DLP

Holly Dickson est maintenant arrivée à un stade de son projet pilote où elle souhaite tester la stratégie DLP concernant les e-mails qui contiennent des informations sensibles, que vous avez créée lors de l’exercice de labo précédent. 

**NOTE :** nous avons rencontré des problèmes intermittents dans le passé de stratégies DLP et de conseils de stratégie DLP ne fonctionnant pas comme prévu dans cet exercice de labo. Ceux-ci sont dus à des problèmes de limitation qui se produisent parfois entre notre environnement de labo sur machine virtuelle et le locataire d’évaluation Microsoft 365. Cela n’est pas représentatif de l’expérience normale des environnements de production Microsoft 365. Cela n’est pas non plus représentatif d’une expérience de formation normale. Nous sommes désolés si vous rencontrez ce problème au cours de cet exercice de labo.

### Tâche 1 - Tester la première règle de stratégie DLP

Dans l’exercice précédent, vous avez créé une stratégie DLP personnalisée qui recherche dans les e-mails des informations sensibles liées aux adresses IP dans votre locataire Adatum. Cette stratégie inclut deux règles : une qui vérifie les e-mails contenant une seule adresse IP, et une autre qui vérifie les e-mails contenant deux adresses IP ou plus. 

Dans cette tâche, vous allez envoyer un e-mail de Holly Dickson à Lynne Robbins qui teste la première règle (adresse IP unique). Lorsque cette règle est déclenchée, un conseil de stratégie d’e-mail s’affiche dans la boîte aux lettres Outlook de l’expéditeur informant l’expéditeur que l’e-mail contient des données sensibles. L’expéditeur reçoit également une notification par e-mail, mais l’e-mail est quand même envoyé au destinataire.

1. Sur LON-CL1, dans votre navigateur Edge, vous devez toujours être connecté à Microsoft 365 en tant que **Holly Dickson**. 

2. Vous allez maintenant envoyer un e-mail de Holly à Lynne Robbins, et inclure une adresse IP dans le corps de l’e-mail. <br/>

    Dans **Microsoft Edge**, sélectionnez l’onglet **Page d’accueil | Microsoft 365**, puis sélectionnez l’icône **Outlook** dans la colonne des icônes d’applications située à gauche de l’écran. Lorsque Outlook sur le web s’ouvre, vous devriez être automatiquement connecté en tant que Holly Dickson.  <br/>

    **Note :** si **Outlook sur le web** était déjà ouvert, vérifiez que vous êtes connecté en tant qu’**Holly** en vérifiant l’icône d’utilisateur située dans le coin supérieur droit (le cercle **HD**). Si Outlook a été ouvert pour un autre utilisateur, fermez l’onglet et répétez les instructions de cette étape pour ouvrir Outlook sur le web pour Holly.

3. Dans le coin supérieur gauche de l’écran, cliquez sur **Nouveau message**. 

4. Dans le volet de message qui s’affiche à droite de l’écran, entrez les informations suivantes :

    - À : entrez **Lynne**, puis sélectionnez **Lynne Robbins** dans la liste des utilisateurs qui s’affiche.

    - Ajoutez un objet : **Test de stratégie DLP 1**.

    - Zone du message : **Salut Lynne, je vais configurer cette adresse IP : 192.168.0.1**.

    **Note :** lorsque vous rédigez cet e-mail en incluant des données sensibles (dans ce cas, une adresse IP), cela déclenche la stratégie liée aux adresses IP que vous avez créée précédemment, en particulier la règle d’adresse IP unique. Par conséquent, un **conseil de stratégie** doit s’afficher indiquant que l’e-mail enfreint une stratégie organisationnelle. Vous allez ignorer ce conseil de stratégie et envoyer l’e-mail quand même afin de tester le reste de la stratégie DLP, qui va envoyer un e-mail de notification à Holly.

5. Lorsque l’info-bulle du conseil de stratégie s’affiche, sélectionnez **Envoyer.**

6. Sélectionnez le dossier **Éléments envoyés** d’Holly pour vérifier que l’e-mail a été envoyé.

7. Sélectionnez le dossier **Boîte de réception** d’Holly. Holly doit recevoir un e-mail de la part de **Microsoft Outlook** avec l’objet : **Notification : Test de stratégie DLP 1**. Sélectionnez cet e-mail et vérifiez son contenu. 

8. Basculez vers **LON-CL2**. 

9. Si vous devez vous connecter à la machine virtuelle, le compte local **LON-CL2\admin** doit apparaître par défaut. Entrez **Pa55w.rd** dans le champ **Mot de passe** pour vous connecter. 

10. Dans la barre des tâches, sélectionnez l’icône du navigateur **Edge**.

11. Dans le navigateur Edge, entrez l’URL suivante : **https://outlook.office365.com**

12. Dans la fenêtre **Choisir un compte**, sélectionnez le compte de Lynne Robbins (**LynneR@xxxxxZZZZZZ.onmicrosoft.com**, où xxxxxZZZZZZ est le préfixe de locataire fourni par votre fournisseur d’hébergement de labo). Dans la fenêtre **Entrer le mot de passe**, entrez le mot de passe du nouvel utilisateur que vous avez attribué au compte de Lynne, puis sélectionnez **Se connecter**. 

13. Dans la fenêtre **Rester connecté**, cochez la case **Ne plus afficher**, puis sélectionnez **Oui**.

14. Dans la boîte de réception de Lynne, vérifiez que cette dernière a bien reçu l’e-mail de Holly Dickson avec l’objet : **Test de stratégie DLP 1**. Sélectionnez le message pour vérifier que le contenu contenant l’adresse IP n’a pas été supprimé. 

15. Laissez l’onglet Outlook ouvert dans le navigateur Edge pour la tâche suivante.

16. Revenez à **LON-CL1**.

    
### Tâche 2 - Tester la deuxième règle de stratégie DLP

Dans l’exercice précédent, vous avez créé une stratégie DLP personnalisée qui recherche dans les e-mails des informations sensibles liées aux adresses IP dans votre locataire Adatum. Cette stratégie inclut deux règles : une qui vérifie les e-mails contenant une seule adresse IP, et une autre qui vérifie les e-mails contenant deux adresses IP ou plus. 
    
Dans cette tâche, vous allez envoyer un e-mail de Holly Dickson à Lynne Robbins qui teste la deuxième règle (plusieurs adresses IP). Lorsque cette règle est déclenchée, un conseil de stratégie d’e-mail s’affiche dans la boîte aux lettres Outlook de l’expéditeur informant l’expéditeur que l’e-mail contient des données sensibles. L’e-mail va être bloqué, mais l’expéditeur peut choisir d’ignorer le blocage de l’e-mail et l’autoriser à être envoyé.  

1. Sur LON-CL1, dans votre navigateur Edge, vous devez toujours être connecté à Microsoft 365 en tant que **Holly Dickson**. 
    
2. Vous allez maintenant envoyer un deuxième message de Holly à Lynne qui contient plusieurs adresses IP. Répétez le processus précédent pour créer un e-mail destiné à Lynne Robbins avec les informations suivantes : 

    - Ajoutez un objet : **Test de stratégie DLP 2**.

    - Zone du message : **Salut Lynne, je vais tester les adresses IP suivantes : 192.168.0.1 et 172.16.0.1**.

    **Note :** lorsque vous rédigez cet e-mail en incluant des données sensibles (dans ce cas, plusieurs adresses IP), cela déclenche la stratégie liée aux adresses IP que vous avez créée précédemment, en particulier la règle d’adresses IP multiples. Par conséquent, un **conseil de stratégie** doit s’afficher indiquant que l’e-mail enfreint une stratégie organisationnelle. Vous allez ignorer ce conseil de stratégie et envoyer l’e-mail quand même afin de tester le reste de la stratégie DLP, qui va bloquer l’e-mail. Une fois que vous avez testé le blocage de l’e-mail, vous allez ignorer le blocage en entrant une justification professionnelle pour l’envoi de ces données sensibles, puis vous allez réessayer d’envoyer l’e-mail.

3. Lorsque l’info-bulle du conseil de stratégie s’affiche, sélectionnez **Envoyer**. Vous devriez immédiatement voir apparaître une boîte de dialogue **Envoi bloqué** qui indique que le message inclut un ou plusieurs destinataires qui ne sont pas autorisés à recevoir des informations sensibles. Cliquez sur **OK**. <br/>

    **Conseil :** en temps normal, vous ignorez le blocage avant l’envoi, mais dans ce cas, nous voulions vous montrer le blocage pour que vous puissiez voir comment il fonctionne. Dans les étapes suivantes, vous allez ignorer le blocage et réessayer d’envoyer l’e-mail.

4. Sélectionnez le dossier **Éléments envoyés** d’Holly pour vérifier que l’e-mail n’a pas été envoyé.

5. Sélectionnez le dossier **Boîte de réception** d’Holly. Notez que l’e-mail ne s’affiche plus. Sélectionnez le dossier** Brouillons** d’Holly, qui contient une copie de l’e-mail. Sélectionnez l’e-mail.

6. Pour envoyer cet e-mail, vous devez ignorer le blocage AVANT de cliquer sur le bouton **Envoyer**. Pour ignorer le blocage, dans l’info-bulle de conseil stratégie qui apparaît en haut du message, sélectionnez **Afficher les détails**.

7. Dans les détails qui s’affichent dans le conseil de stratégie, sélectionnez **Ignorer**.

8. Dans la boîte de dialogue qui s’affiche, l’option **Je possède une justification professionnelle** est sélectionnée par défaut. Laissez cette option sélectionnée et saisissez **Lynne doit être informée des adresses IP que je teste** dans le champ **Saisissez une explication ici**. Sélectionnez **Ignorer**. <br/>

    Notez la manière dont le message du conseil de stratégie a été modifié pour indiquer que vous avez choisi d’envoyer le message même s’il semble contenir des informations sensibles.

9. Sélectionnez le dossier **Éléments envoyés** d’Holly pour vérifier que l’e-mail a été envoyé.

10. Sélectionnez le dossier **Boîte de réception** d’Holly. Holly doit recevoir un e-mail provenant de **Microsoft Outlook** avec l’objet : **Notification : Test de stratégie DLP 2**. Sélectionnez cet e-mail et vérifiez son contenu.
    
11. Basculez vers **LON-CL2**. 

12. Vous devriez toujours être connecté à **Outlook sur le web** sur la machine virtuelle LON-CL2 en tant que **Lynne Robbins**. Dans votre navigateur **Edge**, la boîte aux lettres de Lynne devrait toujours être ouverte dans **Outlook sur le web** dans l’état dans lequel vous l’avez laissée depuis la tâche précédente.

13. Dans la boîte de réception de Lynne, vérifiez qu’elle a reçu l’e-mail de Holly Dickson avec l’objet : **Test de stratégie DLP 2**. Sélectionnez le message pour vérifier que le contenu contenant les adresses IP n’a pas été supprimé. 

14. Laissez l’onglet Outlook ouvert dans le navigateur Edge pour la tâche suivante.

15. Revenez à **LON-CL1**.

    
# Fin du labo 3
