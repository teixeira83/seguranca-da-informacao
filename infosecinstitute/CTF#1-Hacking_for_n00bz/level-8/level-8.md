# Level 8

url: http://ctf.infosecinstitute.com/leveleight.php

## English Version 

### Resolution

In this challenge we have the message: "Do you want to download app.exe file?" Clicking in yes the download starts. 

In terminal:
```
file app.exe
```
> app.exe: PE32 executable (console) Intel 80386 (stripped to external PDB), for MS Windows

Let's see if the is in the strings of executable...

```
strings app.exe | grep flag
```

And there is our flag.

### Flag

```
infosec_flagis_0x1a
```

## Versão em Português

### Resolução

Ao entrar no site recebemos a seguinte mensagem: "Do you want to download app.exe file?" Clicando em yes o download começa. 

No terminal:
```
file app.exe
```
> app.exe: PE32 executable (console) Intel 80386 (stripped to external PDB), for MS Windows

Vamos ver as strings do executável...

```
strings app.exe | grep flag
```

E aqui está nossa flag.

### Flag

```
infosec_flagis_0x1a
```