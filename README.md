# RPG

Le but de cet exercice est de modéliser un RPG via des classes PHP. Le déroulement du jeu n'a aucune importance ainsi que l'équilibre.


## Partie 1

### Configurer Composer pour ajouter l'autoloader

## Implémentation des classes Character.
Pour commencer, il va falloir des personnages dans le jeu qui puissent s'attaquer.

Voici La liste des classes que vous devrez créer et leur spécificité.

### Classe **abstraite** Character

Cette classe dispose des attributs et méthodes suivantes:

**Attributs**:

- name (string)
- health (int)
- attackStrength (int)

**Méthodes**:

- takeDamage : *prend en paramètre un int avec la quantité de dégât*
- attack : *prend en paramètre un Character et lui inflige des dégâts*
- isDead : *renvoi un boolean indiquant si le Character est mort ou non*


### Classe Warrior
Hérite de Character

Cette classe n'a rien de plus, il suffit juste de mettre des valeurs par défaut dans le constructeur.



### Classe Archer
Hérite de Character

Cette classe dispose des attributs et méthodes suivantes :


**Attributs statiques**:

- PRECISION_MAX

**Attributs**:

- precision (int)

**Méthodes**:

- attack : *réécrit la méthode attack du Character pour prendre en compte la precision*

```php
// Details sur l'implémentation de la précision
// Faire aussi simple que ça : on prend un nombre random entre 0 et le max de précision, et on voit si c'est inférieur à la précision
// si c'est inférieur à la précision, alors on a touché la cible, sinon on a manqué.
$hit = rand(0, self::PRECION_MAX) < $this->precision;

if ($hit) {
    $target->takeDamage($this->attackStrength);
}
```

### Classe Wizard

Hérite de Character

**Attributs**:

- mana (int)
- magicAttackBonus (int)
- attackManaCost (int)

**Méthodes**:

- consumeMana : *prend en paramètre une quantité à retirer du mana actuel*
- attack : *Réécris la méthode attack du Character, tant qu'il y a du mana infligé des dégâts de base + dégâts magiques et diminuer le mana. Si plus de mana infliger des dégâts de base.*


### Classe Tank

Hérite de Character

**Attributs**:

- armor (int)

**Méthodes**:

- reduceArmor : *prend en paramètre une quantité à déduire de l'armure*
- takeDamage : *Réécris la méthode takeDamage du Character, pour d'abord diminuer l'armure avant de diminuer la santé*

Testez vos classes sur l'index pour voir tout fonctionne comme souhaité

## Implémentation de l'inventaire

Maintenant, nous avons envie de donner la possibilité a nos Characters de transporter des items et de s'en équiper via un inventaire.

### La classe Inventory

Commençons par créer notre inventaire.

**Attributs**:

- slots (array) *vous pouvez utiliser un tableau associatif : nomItem => item*
- maxWeight (int)

**Méthodes**:

- getItem : *prend en paramètre un index ou une clef et renvoi l'objet Item*
- addItem/storeItem
- removeItem/dropItem
- getTotalWeight : *Renvoi le poids total actuel*
- getTotalWeightPourcentage : *Renvoi le pourcentage actuel d'espace occupé*

### La classe Item

Les items représentent un objet lambda qui peut être stocké dans notre inventaire.

**Attributs**:

- name (string)
- weight (int)

**Méthodes**:

- use : faites la faire ce que vous souhaitez.

### La classe Equipment

Hérite de Item.

La classe équipement, permet de modéliser tout Item pouvant être équipé tel que des armes.

**Attributs**:

- attackBonus (int)
- magicAttackBonus (int)
- armorBonus (int)

**Méthodes**:

Vous pouvez vous montrer créatif, rien n'est attendu en plus.

### Mise à jour de la classe Character

Maintenant que vous disposez d'une classe Inventory et de classes Items. Il faut mettre à jour la classe Character.

**Rajouter les attributs suivants :**
- inventory (Inventory)
- equippedItem (Item)

**Rajouter les méthodes suivantes :**
- Equip : *prend en paramètre une clef ou index à récupérer dans l'inventaire pour l'équiper*

*Modifier les méthodes suivantes :*
 - takeDamage
 - attack

***Si l'equippedItem est un Equipment***, alors deux méthodes doivent prendre en compte les bonus de cet item lors des attaques et prise de dégâts.


Testez les nouvelles fonctionnalités sur l'index.
