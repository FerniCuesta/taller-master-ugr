# Exercise Outcomes Submission Template

**Student/Group Name**: Fernando Cuesta Bueno
**Level Completed**: intermediate
**Date**: 13/02/2026

---

## 📋 Exercise Summary

### Exercise: [Exercise Title]

**Status**: ✅ Completed

**What I did**:

Completé el ejercicio de nivel intermedio donde aprendí a trabajar con fusiones de ramas y resolución de conflictos en Git. Creé dos ramas separadas (`feature/header` y `feature/footer`) a partir de la rama intermedia, añadiendo contenido diferente en cada una en el archivo `page.html`. Luego fusioné ambas ramas en la rama intermedia, descubriendo y resolviendo manualmente el conflicto que surgió al intentar fusionar el contenido superpuesto. Finalmente, practiqué la creación y gestión de etiquetas (tags) en Git, creando etiquetas anotadas y ligeras, visualizando su información y empujándolas al repositorio remoto, entendiendo las diferencias y casos de uso para cada tipo de etiqueta.

**Commands Used**:

**Results/Output**:

```bash
# Commands used to create branches and make conflicting changes
git checkout feature/header
touch page.html
git add page.html
git commit -m "Add header to page"
git checkout feature/footer
touch page.html
git add page.html
git commit -m "Add footer to page"
git checkout intermediate
git merge feature/header
git merge feature/footer # Este comando generará un conflicto
```

```bash
# Output from git merge showing the conflict
git checkout intermediate
git merge feature/header
git merge feature/footer  # This will create a conflict!
Switched to branch 'intermediate'
Your branch is up to date with 'origin/intermediate'.
Updating 994450b..4f99bd1
Fast-forward
 page.html | 20 ++++++++++++++++++++
 1 file changed, 20 insertions(+)
 create mode 100644 page.html
Auto-merging page.html
CONFLICT (add/add): Merge conflict in page.html
Automatic merge failed; fix conflicts and then commit the result.
```

```bash
$ git log --graph --oneline --all
*   e331e2c (HEAD -> group-X-outcomes/intermediate, tag: v1.0-test, tag: v1.0, intermediate) Merge footer with resolved conflicts
|\
| * ff9dacf (feature/footer) Add footer to page
* | 4f99bd1 (feature/header) Add header to page
|/
* 994450b (origin/intermediate) refactor: consolidate intermediate exercises into single comprehensive exercise
* a1c17e7 docs: Add submission instructions to intermediate level
* 9f25f7a Update README for intermediate level exercises
| * d843d3b (origin/group-X-outcomes/newbie, group-X-outcomes/newbie) docs: fill additional comments section
| * baee32c docs: finish newbie documentation
| * 0341b5d add documentation images
| * 0ab09e1 docs: update OUTCOME.md
| * d990c13 docs: Add newbie level exercise outcomes for Group X
| * 360f4a4 (origin/newbie, newbie) refactor: consolidate newbie exercises into single comprehensive exercise
| * 5eedc97 docs: Add submission instructions to newbie level
| * 45e1c31 Update README for newbie level exercises
|/
| * f431f6e (origin/feature/my-info, feature/my-info) Add personal information
| * ea6e83b Allow my-*.txt files in .gitignore
| * 38093d6 (origin/main, origin/HEAD, main) Allow hello.txt in .gitignore
| * 3b826d6 Add hello.txt with my name
| * 9602351 Adding GenAI guidelines
| * 7ad3af4 docs: update main branch files to reflect consolidated exercise structure (1 per level)
| * 4d9131e chore: remove instructor files from repository tracking
| *   adbb307 Merge pull request #9 from miguel-oltra/patch-gitignore-update
| |\
| | * e4709e6 Updated CODEOWNERS file
| | * 2a39a02 chore: add INSTRUCTOR_GUIDE.md to gitignore
| | * 0abdbae chore: add SUMMARY.md to gitignore for instructor files
| |/
| * 88a54ab chore: Add .gitignore to exclude instructor files and sensitive data
| * e39ff08 PROMPT for updated
| * df1cfdd fix: Update CODEOWNERS to allow trainee work while protecting exercise branches
| * a011fad config: Add CODEOWNERS file for code review requirements
| * 769be64 docs: Add complete implementation summary
| * 9d008fa Updated README.MD with guidelines for the exercises
| * f66bf22 docs: Update MODEL_SPEC.MD with PROMPT 2 requirements
| * c24fd57 docs: Add outcome submission process and evaluation criteria
| * ec488d0 Update main README with complete training overview and navigation
|/
| * b0fb9dc (origin/master-of-the-universe) refactor: consolidate master-of-the-universe exercises into single comprehensive exercise
| * d1ef79f docs: Add submission instructions to master-of-the-universe level
| * 5bffa64 Update README for master-of-the-universe level exercises
|/
| * b5d8eb6 (origin/master) refactor: consolidate master exercises into single comprehensive exercise on history rewriting
| * 960a0a6 docs: Add submission instructions to master level
| * f0055a0 Update README for master level exercises
|/
* dc58203 Revert "Update README.md"
* e2db1ca (tag: v0.0.1) Update README.md
* 3d651c3 Update README.md
* 4cc5635 Initial commit
```

```bash
# Commands for creating annotated and lightweight tags
git tag -a v1.0 -m "First stable version with merged features"
git tag v1.0-test
```

```bash
$ git tag
v0.0.1
v1.0
v1.0-test
```

```bash
$ git show v1.0
tag v1.0
Tagger: Fernando Cuesta <fernandocuestab@gmail.com>
Date:   Fri Feb 13 00:41:37 2026 +0000

First stable version with merged features

commit e331e2c8cb8178fa49e04fd46c98cd78a6737ef6 (HEAD -> group-X-outcomes/intermediate, tag: v1.0-test, tag: v1.0, intermediate)
Merge: 4f99bd1 ff9dacf
Author: Fernando Cuesta <fernandocuestab@gmail.com>
Date:   Fri Feb 13 00:41:27 2026 +0000

    Merge footer with resolved conflicts
```

<!-- **Screenshots** (if applicable):

- [Screenshot 1: Description]
- [Screenshot 2: Description] -->

---

## 🎯 Key Learnings

**Main concepts I learned**:

1. Aprendí cómo los conflictos surgen cuando múltiples ramas modifican el mismo archivo y cómo resolverlos manualmente editando el archivo y realizando un commit de merge.

2. Entendí la diferencia entre etiquetas anotadas (`git tag -a`) que contienen metadatos y etiquetas ligeras (`git tag`) que son referencias simples, y su utilidad para marcar versiones.

3. Dominé el uso de flags como `--graph`, `--oneline` y `--all` para obtener una representación clara del árbol de commits y las relaciones entre ramas.

**Skills I improved**:

- Resolución de conflictos de merge
- Gestión de ramas y fusiones
- Creación y gestión de etiquetas en Git

---

## 🚧 Challenges Faced

### Challenge 1: Approaching My First Merge Conflict

**Problem**: Cuando intenté fusionar la rama `feature/footer` en `intermediate`, Git indicó un conflicto en el archivo `page.html`. No sabía exactamente cómo proceder ni qué significaban los marcadores de conflicto que aparecieron en el archivo.

**Solution**: Decidí abrir el archivo en conflicto y analizar los marcadores de conflicto (`<<<<<<<`, `=======`, `>>>>>>>`). Comprendí que estos marcadores indicaban qué cambios venían de cada rama. Luego editué manualmente el archivo para mantener los cambios de ambas ramas (el header y el footer), eliminé los marcadores y realicé un commit de merge. Esto me enseñó que los conflictos no son errores, sino situaciones que requieren decisiones manuales.

**Commands/Approach**:

```bash
# 1. Cuando surgió el conflicto
git merge feature/footer
# CONFLICT (add/add): Merge conflict in page.html

# 2. Inspeccionar el archivo con conflicto
cat page.html

# 3. Editar manualmente para resolver el conflicto
nano page.html

# 4. Marcar como resuelto y completar el merge
git add page.html
git commit -m "Merge footer with resolved conflicts"
```

---

### Challenge 2: Understanding Conflict Markers

**Problem**: Los marcadores de conflicto `<<<<<<<`, `=======` y `>>>>>>>` eran confusos al principio. No entendía claramente qué representaba cada sección del archivo en conflicto.

**Solution**: Aprendí que el contenido entre `<<<<<<<` y `=======` representa los cambios de la rama actual (HEAD), mientras que el contenido entre `=======` y `>>>>>>>` representa los cambios de la rama que se está fusionando. Una vez comprendí esta estructura, pude identificar rápidamente qué cambios mantener, eliminar o combinar. En mi caso, decidí mantener ambos contenidos para tener tanto el header como el footer en la página final.

**Commands/Approach**:

```bash
# Ver el conflicto en el archivo
# <<<<<<< HEAD (rama actual)
# ... contenido del header ...
# =======
# ... contenido del footer ...
# >>>>>>> feature/footer

# Resolver editando el archivo y eliminando los marcadores
git add page.html
git commit -m "Resolve marker conflicts"
```

---

### Challenge 3: Annotated vs. Lightweight Tags

**Problem**: No tenía clara la diferencia entre etiquetas anotadas (`git tag -a`) y etiquetas ligeras (`git tag`), ni cuándo usar cada una. Ambas parecían servir para lo mismo: marcar versiones.

**Solution**: Experimenté creando ambos tipos de tags y usé `git show` para comprender las diferencias. Descubrí que las etiquetas anotadas almacenan metadatos como el autor, la fecha y un mensaje, siendo ideales para versiones estables y releases. Las etiquetas ligeras son solo referencias simples, útiles para marcadores internos o de desarrollo. En mi ejercicio, utilicé `v1.0` como etiqueta anotada para la versión estable y `v1.0-test` como etiqueta ligera para testing, lo que reflejaba perfectamente sus propósitos.

**Commands/Approach**:

```bash
# Crear etiqueta anotada (con metadatos)
git tag -a v1.0 -m "First stable version with merged features"

# Crear etiqueta ligera (solo referencia)
git tag v1.0-test

# Ver información de la etiqueta anotada
git show v1.0

# Ver información de la etiqueta ligera
git show v1.0-test
```

---

### Challenge 4: Finding Resources to Solve Problems

**Problem**: Durante el ejercicio enfrenté varios momentos donde no estaba seguro de cómo proceder, especialmente con la resolución de conflictos y la gestión de tags.

**Solution**: Utilicé múltiples recursos: la documentación oficial de Git (`git help merge`, `git help tag`), ejemplos en línea, y experimentación directa en la terminal. Los comandos `git status` y `git diff` fueron especialmente útiles para entender el estado actual del repositorio. También revisé el historial con `git log --graph` para visualizar la estructura de ramas y entender mejor cómo se relacionaban los commits.

**Commands/Approach**:

```bash
# Consultar la ayuda de Git
git help merge
git help tag

# Ver el estado actual durante un conflicto
git status

# Ver las diferencias en un conflicto
git diff

# Visualizar el árbol de commits y ramas
git log --graph --oneline --all

# Ver información detallada de un commit o tag
git show [ref]
```

---

## 💭 Personal Reflection

**What surprised me**:

Lo que más me sorprendió fue descubrir lo simple que es resolver un conflicto de merge una vez que entiendes la estructura de los marcadores de conflicto.

**What I found most difficult**:

La parte más desafiante fue el momento inicial cuando surgió el conflicto el distinguir los marcadores `<<<<<<<`, `=======` y `>>>>>>>`. Sin embargo, una vez que comprendí la estructura (cambios locales vs cambios remotos), el resto fue más fácil.

**What I found most useful**:

Por lejos, lo más útil fue aprender la resolución de conflictos de merge. Es una habilidad fundamental para cualquier desarrollador que trabaje en equipo.

**How I would apply this in real projects**:

En proyectos reales, usaría estos conocimientos constantemente. Utilizaría un flujo de trabajo con ramas feature (`feature/...`) para cada funcionalidad nueva, sabiendo ahora cómo manejar los conflictos cuando múltiples personas trabajan en el mismo archivo. Las etiquetas las usaría para marcar releases estables (v1.0, v1.1, etc.) usando etiquetas anotadas con mensajes descriptivos. Finalmente, usaría `git log --graph` regularmente para entender el estado del proyecto y comunicarme mejor con mi equipo sobre qué ramas están activas y cómo se relacionan los cambios.

---

## 📊 Self-Assessment

Rate your confidence level for each topic (1-5, where 5 is very confident):

| Topic               | Confidence (1-5) | Notes                                                                                                                                                                                                                    |
| ------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Basic Git commands  | [3]              | Estoy acostumbrado a usar interfaces gráficas, por lo que aún me falta práctica con la terminal.                                                                                                                         |
| Branching & merging | [5]              | En esta práctica me sentí muy cómodo trabajando con ramas, realizando merges y resolviendo conflictos.                                                                                                                   |
| Remote operations   | [5]              | Me siento muy cómodo trabajando con repositorios remotos, haciendo push y pull.                                                                                                                                          |
| Conflict resolution | [5]              |                                                                                                                                                                                                                          |
| History rewriting   | [1]              | Nunca he tenido que reescribir el historial de commits, por lo que no me siento nada seguro con esta práctica.                                                                                                           |
| Git hooks           | [1]              | Nunca he usado Git hooks, por lo que no me siento nada seguro con esta práctica.                                                                                                                                         |
| Security practices  | [2]              | Lo único que he visto de seguridad en Git es el uso herramientas externas que monitorizan el repositorio en busca de posibles vulnerabilidades, pero no tengo experiencia con prácticas de seguridad específicas de Git. |

---

## 🔗 Evidence/Artifacts

**Links to branches/commits**:

- Link to your outcome branch: `https://github.com/miguel-oltra/taller-master-ugr/tree/group-X-outcomes/[level]`
- Key commits demonstrating your work:
  - Commit hash: [Short description]
  - Commit hash: [Short description]

**Additional files created** (if any):

- File 1: [Description]
- File 2: [Description]

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

**Submission Date**: [13/02/2026]

**Ready for Review**: ✅ Yes
