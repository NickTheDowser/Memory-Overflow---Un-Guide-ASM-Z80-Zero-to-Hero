<pre>
     _____                                                                  _____.__                   
    /     \   ____   _____   ___________ ___.__.   _______  __ ____________/ ____\  |   ______  _  __  
   /  \ /  \_/ __ \ /     \ /  _ \_  __ <   |  |  /  _ \  \/ // __ \_  __ \   __\|  |  /  _ \ \/ \/ / 
  /    Y    \  ___/|  Y Y  (  <_> )  | \/\___  | (  <_> )   /\  ___/|  | \/|  |  |  |_(  <_> )     / 
  \____|__  /\___  >__|_|  /\____/|__|   / ____|  \____/ \_/  \___  >__|   |__|  |____/\____/ \/\_/ 
          \/     \/      \/              \/                       \/ 
</pre>

# Memory Overflow - Un Guide ASM Z80 Zero to Hero

## Table des matières
_**TODO**_

## 1.0 Introduction
Memory Overflow - Un Guide ASM Z80 Zero to Hero - est un guide créé de manière collaborative avec le groupe Praline, de la scène demo-making Amstrad CPC, dont le but est de suivre l'apprentissage de l'assembleur pour le processeur Zilog Z80 de Zero to Hero.

Nous allons suivre les pas de Nicolas DESENY [bio sur le site de l'ORCID](https://orcid.org/0009-0002-2113-473X) (à l'origine de ce projet) (aussi appelé "Blood" dans certains passages) dans son apprentissage de l'assembleur pour le processeur Zilog Z80 (Amstrad CPC, Radio Shack TRS-80, Sinclair ZX80 - ZX81 - ZX Spectrum, standard MSX, PC-88....) sous forme de guide avec des exemples pratiques de mise en oeuvre.

Le guide ne contient pas de documentation technique, mais quand nécéssaire, des liens URL vers des sites externes seront disponibles. Des liens Wayback Machine seront également, quand possible, mis en place pour éviter la perte de ces pages et assurer la pérénité de ce guide.

Le présent guide ne prétend pas faire de toi (on va se tutoyer hein) un expert incontestable de l'assembleur pour Zilog Z80, il s'agit surtout d'une aide pour les débutants qui voudraient se lancer. Ce guide demande néanmoins un minimum de bagage et vocabulaire technique pour être compris. tu es averti !

### 1.1 Pourquoi cet ouvrage ?
En travaillant sur une démo pour l'ami RaHoW (body!), je me suis rendu compte, en faisant des recherches, que le savoir de programmer en assembleur sur le Z80 est un savoir qui se perd. Ce qui est logique, lorsqu'on y pense.

Je ne veux surtout pas dénigrer le travail d'archivage et de partage des savoirs entrepris par les membres de la communauté, mais le savoir est éparpillé ça et là. On trouve des bribes, des Wiki, de vraies Bibles écrites par d'illustres cadors, mais qui partent très souvent du principe qu'on sait déjà de quoi on parle; et qui donc n'entrent que très rarement dans le vif du sujet, avec du language technique à vous scier les pattes ! (Souvent on y comprend rien, mais c'est fascinant).

Dans ce guide, on va donc partir du principe que tu ne sais rien, que tu es une page blanche. Ce guide ne s'adresse donc pas aux vétérans, mais vraiment aux débutants. D'au moins 5 ans, de préférence. Tu veux du gâteau mon poussin ?

## X.0 RASM, c'est quoi cette bête ?

Créé par le très talentueux et prolifique Édouard Berger, alias Roudoudou ([Site web de Roudoudou](http://www.roudoudou.com/ACE-DL/)), RASM est un assembleur pour le processeur Z80, et en gros, c'est un outil qui te permet d'écrire des programmes dans un langage que ce processeur peut comprendre. Voici comment ça fonctionne et pourquoi c'est utile :

### X.1 Qu'est-ce que l'assembleur ?

L'assembleur est un type de programme qui traduit le code écrit par les humains (dans un langage compréhensible) en langage machine, que l'ordinateur peut exécuter directement. 

Le langage machine est composé de 0 et de 1, ce qui est super compliqué à écrire à la main. L'assembleur rend tout ça plus accessible. RASM en particulier

***Bulletpoints :***

- **Syntaxe simple :** RASM te permet d'écrire des instructions en utilisant une syntaxe plus compréhensible. Par exemple, au lieu d'écrire des codes hexadécimaux, tu peux écrire des mots comme MOV, ADD, etc. Cela rend la programmation beaucoup plus intuitive.
- **Assemblage :** Quand tu écris ton code dans RASM, tu le "compiles" ou "assembles". Cela signifie que RASM prend toutes les instructions que tu as écrites et les transforme en un fichier exécutable que le Z80 peut comprendre. C'est comme si tu écrivais un script pour une pièce de théâtre, et que RASM s'occupait de le mettre en scène.
- **Erreurs et débogage :** RASM te donne aussi des retours sur ton code. Si tu as fait une erreur, il te le signalera, ce qui est super utile pour apprendre et améliorer tes compétences en programmation.

### X.2 Pourquoi c'est intéressant ?

RASM est intéressant à plus d'un titre. En plus d'être un outil d'assembleur, c'est également une vraie boite à outils avec tout ce dont on peux possiblement avoir besoin (gloire à Roudoudou, son travail est remarquable !!!).

***Bulletpoints :***

- **Apprentissage :** Si tu es passionné par la programmation ou le développement de jeux vidéo, comprendre comment fonctionne un assembleur comme RASM peut te donner une meilleure compréhension de ce qui se passe "sous le capot" de l'ordinateur. 
- **Créativité :** Avec RASM, tu peux créer tes propres programmes, jeux, ou même des démos sur des systèmes qui utilisent le Z80, comme certaines vieilles consoles ou ordinateurs (comme l'Amstrad CPC, le ZX Spectrum ou certaines machines d'arcade). Dans ce guide, on va faire du CPC, mais c'est transposable tant qu'on ne fais rien de très technique (comme les accès disque, gérées par l'os (AmsDos sur CPC) ou l'exploitation de certaines puces spécialisées, comme le CRTC; encore une fois sur Amstrad CPC).
