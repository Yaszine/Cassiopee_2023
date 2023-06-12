# cassiopee-74
Detection de visages sur flux compressé

1ère étape : Récupération des matrices de luminance sur JM Master

  -Ouvrir le logiciel JM Master, faire un build et un run puis lancer les 3 commandes suivantes (penser à modifier le paramètre fp dans le fichier macroblock.c afin de modifier le nom du fichier txt dans lequel seront écrites les matrices voulues)
  
     ffmpeg -i Video.mp4 -c:v libx264 Video.264 
     
     ffprobe -select_streams v -show_frames -v quiet -of csv=p=0 -show_entries frame=pict_type Videoiframe.264 | grep -n I | cut -d ':' -f 1 > Videoiframe.txt

    ./ldecod -i "/path/to/Video.264" -o Video.yuv 
 
 
2ème étape : Conversion en numpy array 

  -Ouvrir le script create_mat.py et décommenter les lignes à la fin. 
  
  -Donner à la variable filename le nom du fichier contenant la matrice extraite précedemment
  
  -Lancer la fonction correct_file(filename)
  
  -Donner à corrected_filename le nom du fichier généré par la fonction correct_file(filename)
  
  -Lancer la fonction create_matrix(corrected_filename)
  
  
3ème étape : Création des masks
  
  -Lancer le script mask_creation.py et modifier le nom du fichier dans la ligne cap = cv2.VideoCapture("Video.mp4") afin de créer les masks depuis la bonne vidéo
  
  -Modifier le paramètre liste_text qui doit contenir la liste des numéros des i frames dans la vidéo
  
  -Par défaut, ce code sauvegardera la matrice des masks sous le nom M.npy


4ème étape : Concaténation
  
  -Répéter les étapes 1 à 3 pour chaque vidéo et concaténer les frames ensembles, puis les masks ensembles
  

5ème étape : Filtrage (étape non obligatoire)
  
  -Cette étape permet de filtrer les données obtenus en ne gardant que les frames où un visage est présent
  
  -Modifier les paramètre data et label pour load les bonnes données
  
  -Décommenter les autres lignes et lancer le code
  
  
  
6ème étape : Training
  
  -Choisir un des 2 modèles (avec ou sans poids ajustés), régler le nom des inputs et lancer l'ensemble du code pour effectuer un training.
  
  
  


