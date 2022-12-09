### Pré-requis: <br/>
Lorsque vous rencontrer `$Text`, cela correspond à une variable, le nom de cette variable explique le champ à remplir. <br/>
Les espaces, majuscule etc dans les parties de code sont à respecter.

# Exercice d'infrastructure
Dans cette exercice, vous allez découvrir comment, de manière simplifié, implémenter un serveur web.<br/> <br/>
Mais tout d'abord, qu'est ce qu'un serveur web? C'est un serveur, une machine, qui va herberger un site web. <br/>
Dans le cas de notre exercice, notre serveur web est un serveur linux. Vous devez être habitué à la maison à utiliser Windows. Linux est un autre système d'opération qui nous permet d'être plus libre dans la création d'un serveur personnalisé (il est open source). Contraiement à windows, nous allons travailler dans cet exercice seulement en invite de commande, c'est à dire que nous n'allons pas avoir d'interface graphique.<br/>
Sur ce serveur Web, nous avons installé le service Apache qui va nous permettre d'afficher notre page web dans un navigateur internet comme Chrome ou Firefox.<br/>

Pour que vous puissiez créer votre propre site web herbergé sur votre serveur web, nous vous proposons de réaliser cet exercice.

 # Création et modification du serveur Web
 
 Pour commencer votre exercice, vous allez devoir vous connecter à distance à votre machine. Une connexion à distance se fait à l'aide de la commande `ssh`. Cette commande nous permet une connexion sécurisé à notre machine distante grâce à un utilisateur (login) et un mot de passe. Nous pouvons comparer cette connexion à celle que vous réaliser sur votre ordinateur personnel. Pour vous connecter à votre machine distante, vous allez entrer la commande suivante: <br/>
 `ssh -p $PORTSsh etudiant@$IP`<br/>
 Entrez `yes` <br/><br/>
 Les variables `$PORTssh` et `$IP` vont vous être communiquées au préalable. Vous êtes maintenant connecté à votre machine distante.
 Nous allons également vous procurer un port pour vous connecter à votre site web, nous allons l'appeler `$PORTSite`. Il est important de le retenir pour la suite du projet.
 
 ### - Se mettre en utilisateur suprême
 Nous allons par la suite devoir entrer des commandes qui peuvent compromettre le serveur. Pour quand même pouvoir les effectuer, nous devons avoir les droits administrateur, c'est à dire devenir l'utilisateur `root` ou un autre utilisateur avec les même droits que lui, dans le même groupe par exemple. Pour passer en utilisateur suprême, nous entrons cette commande dans le terminal:<br/><br/>
 `su -` <br/>Le mot de passe de l'utilisateur root est :`network`<br/><br/>
 **ATTENTION** : Le mot de passe de l'utilisateur suprême n'est jamais sensé être connu de tous, nous vous le donnons pour le bienfait de l'exercice.
 
 ### - Démarrer le service apache
 
 Pour que la page web soit disponible, le service qui permet de l'afficher doit être démarrer, sinon la page à laquelle nous souhaitons accéder sera indisponible.
 Dans votre navigateur, entrer dans la barre de recherche l'adresse IP de votre machine et son port associer.<br/><br/>
 `$IP:$PORTSite`<br/>
 Vous observez que la page n'est pas disponible.<br/>
 Nous pouvons également savoir si le service apache est démarrer sans accéder à la page web. Pour ça, il nous suffit de regarder les ports qui sont "ouverts" (ou en "écoute") sur notre machine. Si vous le fait avant d'avoir démarré le service apache, vous ne devriez pas voir apparaitre le port 80 dans les port ouvert.
 Le port 80 est le port habituel pour le protocole `http` qui sert à accéder à un site web. Pour observer les ports ouvert, entrez la commande:<br/>
 `netsat -an`
 
Dans le terminal, nous allons maintenant démarrer le service apache.<br/><br/>
 `systemctl start apache2`
 
 Si vous retournez dans votre navigateur à la même adresse (il est important de rafraichir la page), vous allez voir la page de démarrage d'apache.<br/>
 Si nous relançons la commande pour regarder les ports ouverts (`netsat -an`), nous observons le port 80 dans la liste, apache est bien démarré. <br/>
 Nous souhaitons créer notre site web, nous allons suppimer cette page web et nous mettrons par la suite notre page personnalisée.<br/>
 
 La page web se trouve dans le dossier `/var/www/html` et se nomme `index.html`. Pour le supprimer, nous allons entrer la commande:<br/><br/>
 `rm /var/www/html/index.html`
 
 ### - Créer un utilisateur et un groupe
 Lors de votre connexion au serveur web, vous allez pouvoir vous créer un utilisateur. Cette utilisateur correspond à votre session. Il est semblable au session de votre ordinateur personnel. Il vous permettra d'avoir votre espace de travail, vos fichiers et dossiers personnels.<br/>
 Pour créer un utilisateur et un groupe à votre nom, nous entrons dans le terminal la commande suivante:<br/><br/>
 `adduser --home /home/$VotreNom $VotreNom`<br/>
   => Entrer le mot de passe de votre choix, retenez le!<br/>
   => Entrer le même mot de passe une deuxième fois<br/>
   => Les informations ne sont que à titre indicatif, vous n'êtes pas obligé de les remplir, appuyer sur `entrer` pour passer<br/>
   => Appuyer sur `y` pour valider la création de votre utilisateur et de votre groupe <br/><br/>
 
 Maintenant que notre utilisateur est créé, nous allons pouvoir continuer l'exercice en tant que cette utilisateur. Nous entrons la commande:<br/><br/>
 `su $VotreNom`
 
 Maintenant, on peut voir que nous sommes connecter avec notre utilisateur. Devant l'espace où vous entrez les commandes, on peut voir:
 `$VotreNom@XXXX:/root$`<br/>
 Cela signifie que vous êtes connecté avec votre utilisateur mais que vous vous trouver dans l'espace de travail de l'utilisateur de `root`.
 
 Toutes les actions de création que nous allons faire appartiendront à notre utilisateur.
 
  ### - Créer un dossier
  
  Nous souhaitons  créer un dossier afin d'y placer notre fichier contenant notre page web. Ce dossier devra se situer dans notre espace de travail.
  Nous allons devoir nous déplacer vers notre espace de travail. En linux, tout déplacement se fait grâce à la commande `cd`. Notre espace personnel s'appelle `/home/$VotreNom`, nous allons donc entrer la commande suivante:<br/><br/>
  `cd /home/$VotreNom`<br/>
  N'hésitez pas à utiliser l'autocomplétion, c'est à dire d'appuyer sur la touche "tabulation". La machine vous montrera les valeurs possibles pour la commande que vous avez commencé à taper.
  
  Maintenant que nous nous situons dans le bon dossier, nous allons en créer un nouveau afin d'y placer notre site web. Pour créer un dossier que nous allons nommer "site_web", nous entrons cette commande:<br/><br/>
  `mkdir site_web`
  
  On peut observer tous les fichiers et dossier présent dans l'espace de travail ou l'on se trouve avec la commande:<br/><br/>
  `ls`<br/>
  En effectuant cette commande, nous pouvons observer que notre dossier s'est bien créé.

### - Copier un fichier
    
  Nous vous déja pré-préparer un site web. Cependant, vous allez quand même devoir légèrement le modifier afin que ca soit votre page web. Cette page se trouve dans le dossier `/home/etudiant/site_web_docker` et se nomme `index.html`. Elle contient les informations qui vont nous etre afficher à l'écrant. Dans se dossier, nous pouvons également voir un fichier qui se nomme `index.css`. C'est la page de style associer à la page html. Elle va permettre de créer le design de la page. 
Avnt de modifier notre site web, nous allons d'abord le copier dans notre dossier. Pour ça, nous lançons la commande:<br/>
`cp /home/etudiant/index.html site_web/index.html`<br/><br/>
Nous devons également copier le fichier de style, nous lançons donc la commande:<br/>
`cp /home/etudiant/index.css site_web/index.css`<br/><br/>
Maintenant, si nous nous déplaçons dans le dossier `site_web` et que nous observons tous les fichiers présents, nous pouvons voir nos deux fichiers qui va créer notre page web.<br/>
`cd site_web`<br/>
`ls`<br/>

### - Modifier notre site web

Nous allons modifier le site web afin qu'il vous soit personnalisé. Pour ça, nous allons modifier le fichier `index.html`. Entrez la commande:<br/>
`nano index.html`

Une fois que vous vous trouvez dans le fichier, vous allez vous trouver face à un grand nombre d'information. La plupart sont la syntaxe du fichier `.html`. Nous n'allons pas nous en préoccuper. Vous allez voir deux lignes d'étoiles avec un texte entre. Suivez l'instruction (écrivez votre prénom sous les lignes d'étoiles mais avant la ligne `</h1></div>`.
Une fois ce la fait, vous pouvez quitter en fichier en appuyant sur les touches `ctrl` et `X` en même temps et appuyer sur la touche `Y` pour valider vos modifications.

### - Afficher la page web dans notre navigateur

Une fois que nos fichiers sont modifiés à notre convenance, nous allons les afficher dans notre navigateur. Comme nous l'avons expliqué ci-dessus, pour que nous puissions afficher une page web dans le navigateur, elle doit se trouver dans le dossier `/var/www/html`. Nous allons donc copier les deux fichiers qui composent notre page web dans ce dossier.<br/>
`cp index.html /var/www/html/index.html`<br/>
`cp index.css /var/www/html/index.css`<br/>

Nous allons rafraichir la page dans notre navigateur qui était à l'adresse : `$IP:$PORTSite`

Vous observer votre page web? <br/>
# BRAVO, vous avez réussi!
