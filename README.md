# keyboard_howto

# Touches magiques SysRq
Les magic [SysRq](https://www.kernel.org/doc/html/latest/admin-guide/sysrq.html) (Systèm Request : requête système) keys sont des combinaisons de touches type *Alt + SysRq + Touche* permettant d'envoyer des commandes de bas niveau directement au noyau. ([source](https://debian-facile.org/doc:systeme:touches-magiques))

Remarque : sur un clavier AZERTY, la touche "SysRq" est la touche "Impression écran système"

Conseil important : 
attendre plusieurs secondes entre les différentes combinaisons de touches, 
car en cas de plantage sévère vous ne verrez pas les messages de progression s'afficher... ([source](https://www.debian.org/doc/manuals/debian-reference/ch09.fr.html#_alt_sysrq_key))
## Linux Debian Stretch
### Magic SysRq est-il activé ?
```sh
user@host:~# cat /proc/sys/kernel/sysrq
1
```
[source](https://www.debian.org/doc/manuals/debian-reference/ch09.fr.html#_alt_sysrq_key)

Nota : la valeur retournée est la combinaison des fonctionnalités autorisées (voir [Fonctionnalités SysRq](#func_sysrq))
### <a name="func_sysrq"></a> Fonctionnalités SysRq
La valeur de /proc/sys/kernel/sysrq (voir dessus) indique les fonctionnalités actives de SysRq : 0 SysRq est désactivé, 1 SysRq est activé, 
&gt;1 seuls les fonctionnalités des bits à 1 sont activées ([source](https://www.kernel.org/doc/html/latest/admin-guide/sysrq.html#how-do-i-enable-the-magic-sysrq-key))
### Commandes SysRq
Voir [ici](https://www.kernel.org/doc/html/latest/admin-guide/sysrq.html#what-are-the-command-keys)
### Activer/Désactiver temporairement
```sh
user@host:~# echo 1 > /proc/sys/kernel/sysrq
```
Nota : pour choisir les fonctions temporaires possibles, se référer à [Fonctionnalités SysRq](#func_sysrq)

[source](https://www.debian.org/doc/manuals/debian-reference/ch09.fr.html#_alt_sysrq_key)
### Rendre permanent
Ajouter la ligne ```kernel.sysrq=1``` dans ```/etc/sysctl.conf```

[source](https://www.debian.org/doc/manuals/debian-reference/ch09.fr.html#_alt_sysrq_key)

Nota : pour choisir les fonctions permanentes à appliquer, se référer à [Fonctionnalités SysRq](#func_sysrq)
### Se tirer d'une situation désastreuse
"La combinaison de « Alt-Sys s », « Alt-Sys u » et « Alt-Sys r » permet de se tirer de situation vraiment désastreuse et obtenir à nouveau l'accès à un clavier opérationnel sans avoir à arrêter le système." ([source](https://www.debian.org/doc/manuals/debian-reference/ch09.fr.html#_alt_sysrq_key))

Nota : Les touches magiques ne tiennent pas compte de la disposition de votre clavier et sont basées sur le layout QWERTY ([source](http://doc.ubuntu-fr.org/touches_magiques#les_combinaisons_de_touches)), ce qui n'est pas le cas des touches S, U et R ([wikipédia](https://en.wikipedia.org/wiki/Magic_SysRq_key#Commands))

## Alternative à AltGr
Sous Windows, sur un clavier AZERTY on peut taper backslash sans bouger les doigts en remplacant AltGr par Ctrl gauche + Alt gauche

Ainsi Ctrl gauche + Alt gauche + 8 tape le backslash

ATTENTION : la solution présenté ici a marché pour Ubuntu 16.04 LTS 64 bits mais pas sous Debian Buster
=> solution temporaire /media/lnj/DATA/projets/linux/keyboard/ctrl_alt_to_altgr avec Hotkey
=> voir aussi toute la recherche que j'ai faite pour réussir à faire fonctionner xkb mais qui n'a pas abouti car type non détecté par debug xkb (voir lien ArchLinux) MAIS symbole "fr" exécute bien la partie (?) latin9 car si je change A en Z, lorsque je redémarre "systemctl restart desktop-manager" (de mémoire) A est bien transformé en Z

https://unix.stackexchange.com/questions/157834/how-to-bind-altgr-to-ctrl-alt/187495#187495

https://web.archive.org/web/20150403042123/http://www.charvolant.org/~doug/xkb/html/xkb.html

http://linux.lsdev.sil.org/wiki/index.php/Building_an_XKB_Keyboard

Non étudiés : 

https://wiki.archlinux.org/index.php/X_keyboard_extension#Caps_hjkl_as_vimlike_arrow_keys

https://www.x.org/releases/X11R7.7/doc/kbproto/xkbproto.html

TODO : trouver solution pour l'intégrer au dessus du serveur X

J'ai trouvé une solution acceptable [ici](https://unix.stackexchange.com/questions/84707/how-can-i-make-ctrl-alt-act-like-alt-gr-in-ubuntu/184886#184886)
et voici mon fichier de mappage :
```sh
user@host:~$ cat ~/.xbindkeysrc
"xvkbd -xsendevent -text '|'"
    m:0xc + c:15
    Control+Alt + 6

"xvkbd -xsendevent -text '`'"
    m:0xc + c:16
    Control+Alt + 7

"xvkbd -xsendevent -text '\\'"
    m:0xc + c:17
    Control+Alt + 8

"xvkbd -xsendevent -text '^'"
    m:0xc + c:18
    Control+Alt + 9

"xvkbd -xsendevent -text '@'"
    m:0xc + c:19
    Control+Alt + 0

"xvkbd -xsendevent -text ']'"
    m:0xc + c:20
    Control+Alt + ssharp

"xvkbd -xsendevent -text '}'"
    m:0xc + c:21
    Control+Alt + equal
```
Pour appliquer utiliser```killall xbindkeys ; xbindkeys -f ~/.xbindkeysrc```

Nota : On supprime tous les autres processus liés avant de recharcher la configuration

Pour [identifier](https://wiki.archlinux.org/index.php/Xbindkeys#GUI_method) une combinaison de touche utiliser ```xbindkeys --multikey ```


