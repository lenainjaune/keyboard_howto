# keyboard_howto

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


