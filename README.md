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
 
 Pour la création de votre serveur web, nous allons vous lancer un conteneur qui fera office de serveur. Lors du lancement du conteneur, vous allez directement y être connecté. Il va être important de garder le port de votre conteneur. Dans la commande "docker run", retenez l'information à la place des XXXX: <br/><br/>
 `-p XXXX:80` <br/><br/>
 C'est le port sur lequel est exposé votre serveur web, il nous permettra par la suite d'avoir accès à notre page web sur le navigateur.
 
 ### - Se mettre en utilisateur suprême
 Nous allons par la suite devoir entrer des commandes qui peuvent compromettre le serveur. Pour quand même pouvoir les effectuer, nous devons avoir les droits administrateur, c'est à dire devenir l'utilisateur `root` ou un autre utilisateur avec les même droits que lui, dans le même groupe par exemple. Pour passer en utilisateur suprême, nous entrons cette commande dans le terminal:<br/><br/>
 `su -` <br/>
 
 Vous avez peut être remarqué que vous utilisiez deja l'utilisateur root, mais cela n'est pas toujours le cas!
 
 ### - Créer un utilisateur et un groupe
 Lors de votre connexion au serveur web, vous allez pouvoir vous créer un utilisateur. Cette utilisateur correspond àvotre session. Il est semblable au session de votre ordinateur personnel. Il vous permettra d'avoir votre espace de travail, vos fichiers et dossiers personnels.<br/>
 Pour créer un utilisateur et un groupe à votre nom, nous entrons dans le terminal la commande suivante:<br/><br/>
 `adduser --home /home/$VotreNom $VotreNom`<br/>
   => Entrer le mot de passe de votre choix, retenez le!<br/>
   => Entrer le même mot de passe une deuxième fois<br/>
   => Les informations ne sont que à titre indicatif, vous n'êtes pas obligé de les remplir<br/>
   => Appuyer sur `y` pour valider la création de votre utilisateur et de votre groupe <br/><br/>
 
 Maintenant que notre utilisateur est créé, nous allons pouvoir continuer l'exercice en tant que cette utilisateur. Nous entrons la commande:<br/><br/>
 `su $VotreNom`
 
 Maintenant, on peut voir que nous sommes connecter avec notre utilisateur. Devant l'espace ou vous entrez les commandes, on peut voir:
 `$VotreNom@XXXX:/root$`<br/>
 Cela signifie que vous êtes connecté avec votre utilisateur mais que vous vous trouver dans l'espace de travail de l'utilisateur de `root`.
 
 Toutes les actions de création que nous allons faire appartiendront à notre utilisateur.
 
  ### - Créer un dossier
  
  Nous souhaitons  créer un dossier afin d'y placer notre fichier contenant notre page web. Ce dossier devra se situer dans notre espace de travail.
  Nous allons devoir nous déplacer vers notre espace de travail. En linux, tout déplacement se fait grâce à la commande `cd`. Notre espace personnel s'appelle `/home/$VotreNom`, nous allons donc entrer la commande suivante:<br/><br/>
  `cd /home/$VotreNom`
  
  Maintenant que nous nous situons dans le bon dossier, nous allons en créer un nouveau afin d'y placer notre site web. Pour créer un dossier que nous allons nommer "site_web", nous entrons cette commande:<br/><br/>
  `mkdir site_web`
  
  On peut observer tous les fichiers et dossier présent dans l'espace de travail ou l'on se trouve avec la commande:<br/><br/>
  `ls`<br/>
  En effectuant cette commande, nous pouvons observer que notre dossier s'est bien créé.
