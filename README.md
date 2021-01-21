# keyboard_howto

## Alternative à AltGr
Sous Windows, sur un clavier AZERTY on peut taper backslash sans bouger les doigts en remplacant AltGr par Ctrl gauche + Alt gauche

Ainsi Ctrl gauche + Alt gauche + 8 tape le backslash

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
