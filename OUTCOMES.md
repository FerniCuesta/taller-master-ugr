# Exercise Outcomes Submission Template

**Student/Group Name**: Fernando Cuesta Bueno
**Level Completed**: newbie
**Date**: 12 de Febrero de 2026

---

## 📋 Exercise Summary

### Exercise: Newbie

**Status**: ✅ Completed

**What I did**:
En esta introducción a Git hemos realizado la configuración inicial de Git, incluyendo la creación de un repositorio local y la realización de commits básicos. También hemos aprendido a crear ramas y subirlas a un repositorio remoto en GitHub.

**Commands Used**:

```bash
# List the key Git commands you used across all parts of the exercise
git config --global user.name "Fernando Cuesta"
git config --global user.email "fernandocuestab@gmail.com"
git clone git@github.com:FerniCuesta/taller-master-ugr.git
touch hello.txt
git status
git add hello.txt
git commit -m "Add hello.txt with my name"
git log
git checkout -b feature/my-info
touch my-info.txt
git add my-info.txt
git commit -m "Add personal information"
git remote -v
git remote set-url origin https://github.com/FerniCuesta/taller-master-ugr
git push origin feature/my-info
git checkout newbie
git push -u origin newbie
git pull origin newbie
git checkout -b group-X-outcomes/newbie
git checkout main -- OUTCOME_TEMPLATE.md
# etc.
```

**Results/Output**:

```
$ git checkout
feature/my-info                 master-of-the-universe          origin/master
FETCH_HEAD                      newbie                          origin/master-of-the-universe
HEAD                            ORIG_HEAD                       origin/newbie
intermediate                    origin/HEAD                     v0.0.1
main                            origin/intermediate
master                          origin/main
```

```
$ git checkout feature/my-info
Switched to branch 'feature/my-info'
```

```
$ git checkout feature/my-info
Switched to branch 'feature/my-info'
```

```
$ git add my-info.txt
git commit -m "Add personal information"
[feature/my-info f431f6e] Add personal information
 1 file changed, 3 insertions(+)
 create mode 100644 my-info.txt
```

```
$ git push origin feature/my-info
Enumerating objects: 8, done.
Counting objects: 100% (8/8), done.
Delta compression using up to 16 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 667 bytes | 667.00 KiB/s, done.
Total 6 (delta 3), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (3/3), completed with 2 local objects.
remote:
remote: Create a pull request for 'feature/my-info' on GitHub by visiting:
remote:      https://github.com/FerniCuesta/taller-master-ugr/pull/new/feature/my-info
remote:
To github.com:FerniCuesta/taller-master-ugr.git
 * [new branch]      feature/my-info -> feature/my-info
```

```
$ git checkout newbie
branch 'newbie' set up to track 'origin/newbie'.
Switched to a new branch 'newbie'
```

```
$ git pull origin newbie
From github.com:FerniCuesta/taller-master-ugr
 * branch            newbie     -> FETCH_HEAD
Already up to date.
```

```
$ git checkout newbie
Already on 'newbie'
```

```
$ git checkout -b group-X-outcomes/newbie
Your branch is up to date with 'origin/newbie'.
Switched to a new branch 'group-X-outcomes/newbie'
```

<!-- **Screenshots** (if applicable):

- [Screenshot 1: Description]
- [Screenshot 2: Description] -->

---

## 🎯 Key Learnings

**Main concepts I learned**:

1. Cómo configurar Git con mi nombre y correo electrónico.
2. Cómo clonar un repositorio y subir cambios a un repositorio remoto.
3. Cómo crear ramas y moverme entre ellas.

**Skills I improved**:

- Usar git por terminal, ya que estoy acostumbrado a usar interfaces gráficas.
- Crear una rama en local y subirla a GitHub.
- Crear un fork de un repositorio y trabajar con él.

---

## 🚧 Challenges Faced

### Challenge 1: Clonar el repositorio sin hacer un fork

**Problem**: En la descripción original de la práctica no se menciona que haya que hacer un fork del repositorio, sino que se clona directamente. Esto me llevó a cometer un error al intentar subir mis cambios, ya que no tenía permisos para hacerlo en el repositorio original.

**Solution**: Para resolver este problema, tuve que crear un fork del repositorio en mi cuenta de GitHub, clonar ese fork en mi máquina local, hacer mis cambios allí y luego subirlos a mi fork.

<!-- **Commands/Approach**:

```bash
# Commands or approach used to solve the problem
``` -->

---

### Challenge 2: Subir archivos ubicados en el .gitignore

**Problem**: Tras realizar los pasos que propone la práctica, me di cuenta de que los archivos que había creado (hello.txt y my-info.txt) no se podían committear ni subir al repositorio porque estaban listados en el archivo .gitignore del repositorio, lo que me impedía completar la práctica correctamente.

**Solution**: Para solucionar este problema, tuve que modificar el archivo .gitignore para eliminar las líneas que ignoraban esos archivos, lo que me permitió añadirlos al staging area, hacer commit y subirlos al repositorio remoto.

---

## 💭 Personal Reflection

**What surprised me**:
He descubierto que Git es mucho más poderoso y flexible de lo que pensaba. No sabía la cantidad de información que proporciona el comando `git log`.

**What I found most difficult**:
Al llevar años usando interfaces gráficas para Git, me costó acostumbrarme a usar la terminal y recordar los comandos exactos.

**What I found most useful**:
Aprender a crear ramas y subirlas a GitHub es una habilidad fundamental que me será muy útil en cualquier proyecto de desarrollo de software.

**How I would apply this in real projects**:
En mi día a día como desarrollador, usaré (y uso) Git para gestionar el código de mis proyectos, así como para colaborar con otros desarrolladores.

---

## 📊 Self-Assessment

Rate your confidence level for each topic (1-5, where 5 is very confident):

| Topic               | Confidence (1-5) | Notes                                                                                                                                                                                                                    |
| ------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Basic Git commands  | [3]              | Estoy acostumbrado a usar interfaces gráficas, por lo que aún me falta práctica con la terminal.                                                                                                                         |
| Branching & merging | [4]              | Me siento cómodo creando ramas y moviéndome entre ellas, aunque aún me falta práctica con los conflictos de merge.                                                                                                       |
| Remote operations   | [5]              | Me siento muy cómodo trabajando con repositorios remotos, haciendo push y pull.                                                                                                                                          |
| Conflict resolution | [4]              | Hay ocasiones en las que resolver conflictos se me complica, pero en general me siento cómodo con ello.                                                                                                                  |
| History rewriting   | [1]              | Nunca he tenido que reescribir el historial de commits, por lo que no me siento nada seguro con esta práctica.                                                                                                           |
| Git hooks           | [1]              | Nunca he usado Git hooks, por lo que no me siento nada seguro con esta práctica.                                                                                                                                         |
| Security practices  | [2]              | Lo único que he visto de seguridad en Git es el uso herramientas externas que monitorizan el repositorio en busca de posibles vulnerabilidades, pero no tengo experiencia con prácticas de seguridad específicas de Git. |

---

## 🔗 Evidence/Artifacts

**Links to branches/commits**:

- Link to your outcome branch: `https://github.com/FerniCuesta/taller-master-ugr/tree/newbie`
- Key commits demonstrating your work:
  - Commit hash: [Short description]
  - Commit hash: [Short description]

<!-- **Additional files created** (if any):

- File 1: [Description]
- File 2: [Description] -->

---

## ✅ Completion Checklist

Before submitting, ensure you have:

- [ ] Completed the exercise for your chosen level (including all parts)
- [ ] Documented all commands used with their outputs
- [ ] Described challenges and how you resolved them
- [ ] Provided a thoughtful reflection on your learning
- [ ] Self-assessed your confidence in each topic
- [ ] Pushed your outcome branch to the remote repository
- [ ] Created a Pull Request (if required by your instructor)

---

## 📝 Additional Comments

[Any additional thoughts, questions, or feedback about the exercises]

---

**Submission Date**: [Date]  
**Ready for Review**: ✅ Yes / ❌ No
