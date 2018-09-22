# Notas sobre os comandos inciais do Git

### …or create a new repository on the command line
```
echo "# notas-docker" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/msilva1610/notas-docker.git
git push -u origin master

```
### …or push an existing repository from the command line

```
git remote add origin https://github.com/msilva1610/notas-docker.git
git push -u origin master
```

### git setup login
```
git config --global user.name "msilva1610"
git config --global user.email "johndoe@example.com"
git config --global core.editor code
```
### Comando para evitar username e password

```
git config --global credential.helper osxkeychain
```
