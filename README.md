### Pré-requis: <br/>
Lorsque vous rencontrer `$Text`, cela correspond à une variable, le nom de cette variable explique le champ à remplir. <br/>
Les espaces, majuscule etc dans les parties de code sont à respecter.

# Exercice d'infrastructure
Dans cette exercice, vous allez découvrir comment, de manière simplifié, implémenter un serveur web.<br/> <br/>
Mais tout d'abord, qu'est ce qu'un serveur web? C'est un serveur, une machine, qui va herberger un site web. <br/>
Dans le cas de notre exercice, notre serveur web est un serveur linux. Vous devez être habitué à la maison à utiliser Windows. Linux est un autre système d'opération qui nous permet d'être plus libre dans la création d'un serveur personnalisé (il est open source). <br/>
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
  => Les informations ne sont que à titre indicatif, vous n'etes pas obligé de les remplir<br/>
  => Appuyer sur `y` pour valider la création de votre utilisateur et de votre groupe <br/><br/>
 
 Maintenant que votre utilisateur est créé, nous allons l'associer à un groupe afin qu'il récupère les droits de ce groupe. Nous souhaintons que notre utilisateur est les droits administrateur afin de pouvoir réaliser nos commandes, nous allons donc associer notre utilisateur au groupe `root`. Pour faire ça, nous entrons la commande suivante:<br/><br/>
 `adduser $VotreNom root`
 
 Maintenant que notre utilisateur est créé et qu'il est dans le groupe de root, nous allons pouvoir continuer l'exercice en tant que cette utilisateur. Nous entrons la commande:
 `su $VotreNom`
 
 Maintenant, on peut voir que nous sommes connecter avec notre utilisateur. Toutes les actions de création que nous allons faire seront à notre utilisateur.
 
  ### - Créer un dossier
