# Stage
Configuration de l'environnement(MSYS2,Gtkmm,ECLIPSE,GLADE)
## Configuration du MSYS2
https://www.msys2.org/ \
https://www.devdungeon.com/content/install-gcc-compiler-windows-msys2-cc \
Les problèmes possibles : \
1/ éxecuter $ pacman -Sy avant $ pacman -Su 

## Variables d'environnement
•	MINGW_HOME C:\msys64\mingw64\
•	MSYS_HOME C:\msys64\
•	PKG_CONFIG_PATH \msys64\mingw64\bin\

!! La variable d'environnement PATH(Windows) n'est pas héritée de msys2.\
!! Comment accéder aux variables d'environnement Windows sur MSYS2? \
Solution: \ Modifier le fichier msys2_shell.cmd en ajoutant \
set MSYS=winsymlinks:nativestrict \
set MSYS2_PATH_TYPE=inherit 

==>Installer des packages(gcc,g++,...), et jouer avec les commandes sous MSYS2-64 ou windows power shell pour verifier que tout fonctionne. 

## Gtkmm(3.0) sous windows 
https://wiki.gnome.org/Projects/gtkmm/MSWindows \
Aprés l'installation des packages nécessaires(Version 64 dans notre cas) \
!! L'installation du pkg-config (pkg-config 0.29.2-4) est nécessaire pour la suite. \
Notice: 
Si la commande $pkg-config --cflags --libs gtkmm-3.0 n'affiche pas le nécessaire en utilisant le PS du windows ça posera pas un probleme. 

Ouvrir MSYS2-64 bash et tester avec la commande: \
g++ foo.cpp -o target.exe `pkg-config gtkmm-3.0 --cflags –libs` 
Notice: Le fonctionnement avec PS windows n'est pas obligatoire. 
### Problème :
$pkg-config fonctionne bien sur le MSYS2 64 mais pas sur un terminal Windows. \
$pkg-config --list-all ==> Detecte que les packages (.pc) qui se trouvent dans le fichier /usr/lib/pkgconfig/"packageName".pc
### Solution:
Accédez à C:\msys64\mingw64\lib\pkgconfig\”packageName”.pc \
Copiez les fichiers dans le dossier Windows. \
Essayez d'exécuter un simple programme gtkmm avec le terminal Windows.

## Eclipse
Integrer MSYS2 dans eclipse. \
https://www.devdungeon.com/content/how-setup-gcc-msys2-eclipse-windows-c-development

--/ Pour les librairies et dependances.
Filtrer tout les dépendances qui concernent gtkmm-3.0.\
$pkg-config –libs --flags gtkmm-3.0 > /home/alayo/tests/output
Toutes les dépendances sont maintenant enregistrées dans un fichier.\
Il faut justement effacer les parametres du liaison et copier les dépendance dans eclipse.

# Glade
https://packages.msys2.org/package/mingw-w64-x86_64-glade
Juste pour tester : \
https://stackoverflow.com/questions/49629744/gtk-glade-aide-destroy-signal-problems
Si vous utilisez l'environnement MS Windows, nous devons ajouter G_MODULE_EXPORT lors de l'appel d'un action handler (programmation C et non gtkmm (C ++))

!!! Problème persistant avec la libxml++ -« version » 
1. Libxml++ dépend de libxml2 et de lui-même 
2. Libxml2 est dans sa version stable : 2.9.10 (30 octobre 2019; il y a 18 mois) 
3. Essayer avec différentes versions de libxml ++ (entre le 22-05-2020 et le 28-08-2020) 

### Commandes Utiles
$ pacman -Q | grep gtkmm ==> Trouver le package et sa version. 

## Trello et documentation
https://trello.com/b/jMCgu521/demarches
