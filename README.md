# Découpage de réseaux IP

## Généralités
Une société fictive a 4 pôles informatiques. Le réseau est en 172.16.1.0/24.
Découper ce réseau de 2 manières, symétrique et asymétrique, pour que chaque pôle ci-dessous puissent avoir assez d'adresse pour chaque équipement.

  * **Sous-réseau 1** : _Le Pôle informatique (6 bureaux, environ 50 équipements au total)_
  * **Sous-réseau 2** : _Le Pôle développement (6 bureaux, environ 12 équipements au total)_
  * **Sous-réseau 3** : _Le Pôle Administratif (4 bureaux, environ 20 équipements au total)_
  * **Sous-réseau 4** : _Le Pôle Technicien (4 bureaux, environ 15 équipements au total)_

## Découpage symétrique
Chaque sous-réseau seront de taille symétrique et devra au moins accueillir 50 équipements. <br>
Pour calculer l'adresse de début et de fin, il faut faire attention à ne pas faire qu'une simple addition. Par exemple si le début est à 172.16.1.65, pour avoir nos 62 adresses il faut faire +61 car nous avons déjà une adresse avec la 65!<br>
### Calcul du CIDR
On calcul le CIDR en prenant le chiffre de la puissance, soit : 2^6 = 64, _cela permettra d'accueillir les 50 équipements sans oublier les adresses réseau et de broadcast_.<br>
Ensuite, il faut enlever le nombre de bits hôte, soit : 32-6 = 26, cela donne un CIDR de /26.
### Découpage des sous-réseaux
  * Sous-réseau 1

Adresse de réseau | Adresse de début | Adresse de fin | Adresse de broadcast
--- | --- | --- | ---
172.16.1.0/26 | 172.16.1.1 | 172.16.1.62 | 172.16.1.63

  * Sous-réseau 2

Adresse de réseau | Adresse de début | Adresse de fin | Adresse de broadcast
--- | --- | --- | ---
172.16.1.64/26 | 172.16.1.65 | 172.16.1.126 | 172.16.1.127

  * Sous-réseau 3

Adresse de réseau | Adresse de début | Adresse de fin | Adresse de broadcast
--- | --- | --- | ---
172.16.1.128/26 | 172.16.1.129 | 172.16.1.190 | 172.16.1.191

  * Sous-réseau 4

Adresse de réseau | Adresse de début | Adresse de fin | Adresse de broadcast
--- | --- | --- | ---
172.16.1.192/26 | 172.16.1.193 | 172.16.1.254 | 172.16.1.255

## Découpage asymétrique
Contrairement au découpage symétrique, où chaque plage d'adresse est identique en quantité, le découpage asymétrique a une d'adresse proportionnelle à la demande de chaque sous-réseau.
### Calcul du CIDR
La méthode de calcul ne change pas, cependant nous devons calculé le CIDR pour chaque sous-réseau :
  * Sous-réseau 1
    * Besoin de 50 équipements
    * 2^6 = 64
    * 64-2 = 62 adresses disponibles pour ce réseau
    * 32-6 = 26
    * Ce sous-réseau a un CIDR /26
  * Sous-réseau 2
    * Besoin de 12 équipements
    * 2^4 = 16
    * 16-2 = 14 adresses disponibles pour ce réseau
    * 32-4 = 28
    * Ce sous-réseau a un CIDR /28
  * Sous-réseau 3
    * Besoin de 20 équipements
    * 2^5
    * 32-2 = 30 adresses disponibles pour ce réseau
    * 32-5 = 27
    * Ce sous-réseau a un CIDR /27
  * Sous-réseau 4
    * Besoin de 15 équipements
    * 2^5
    * 32-2 = 30 adresses disponibles pour ce réseau
    * 32-5 = 27
    * Ce sous-réseau a un CIDR /27
### Découpage des sous-réseaux
Comme pour le découpage symétrique, il faut faire attention aux additions pour les adresses de début et de fin.<br>
Attention, lors d'un découpage asymétrique, il faut commencer avec le sous-réseau qui a le plus d'adresse et finir par celui qui en a le moins.<br>

  * Sous-réseau 1

Adresse de réseau | Adresse de début | Adresse de fin | Adresse de broadcast
--- | --- | --- | ---
172.16.1.0/26 | 172.16.1.1 | 172.16.1.62 | 172.16.1.63

  * Sous-réseau 3

Adresse de réseau | Adresse de début | Adresse de fin | Adresse de broadcast
--- | --- | --- | ---
172.16.64./27 | 172.16.1.65 | 172.16.1.94 | 172.16.1.95

  * Sous-réseau 4

Adresse de réseau | Adresse de début | Adresse de fin | Adresse de broadcast
--- | --- | --- | ---
172.16.1.96/27 | 172.16.1.97 | 172.16.1.126 | 172.16.1.127

  * Sous-réseau 2

Adresse de réseau | Adresse de début | Adresse de fin | Adresse de broadcast
--- | --- | --- | ---
172.16.1.128/28 | 172.16.1.129 | 172.16.1.142 | 172.16.1.143
