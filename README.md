# Exercice d'infrastructure
Dans cette exercice, vous allez découvrir comment, de manière simplifié, implémenter un serveur web.<br/> <br/>
Mais tout d'abord, qu'est ce qu'un serveur web? C'est un serveur, une machine, qui va herberger un site web. <br/>
Dans le cas de notre exercice, notre serveur web est un serveur linux. Vous devez être habitué à la maison à utiliser Windows. Linux est un autre système d'opération qui nous permet d'être plus libre dans la création d'un serveur personnalisé (il est open source). <br/>
Sur ce serveur Web, nous avons installé le service Apache qui va nous permettre d'afficher notre page web dans un navigateur internet comme Chrome ou Firefox.<br/>

Pour que vous puissiez créer votre propre site web herbergé sur votre serveur web, nous vous proposons de réaliser cet exercice.

 # Création et modification du serveur Web
 
 Pour la création de votre serveur web, nous allons vous lancer un conteneur qui fera office de serveur. Lors du lancement du conteneur, vous allez directement y être connecté. Il va être important de garder le port de votre conteneur. Dans la commande "docker run", retenez l'information en gras: <br/>
 " -p ***XXXX***:80 " <br/>
 C'est le port sur lequel est exposé votre serveur web, il nous permettra par la suite d'avoir accès à notre page web sur le navigateur.
 
 Lors de votre connexion au serveur web, vous allez devoir vous créer un utilisateur. 
