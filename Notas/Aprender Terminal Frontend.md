# 🧪 Semana 1 - Terminal para Frontend Devs en macOS

Guía práctica para dominar lo esencial de la terminal usando Zsh + iTerm2 + Oh My Zsh.

---

## ✅ Día 1: Navegación y archivos

- [ ] `pwd` – Ver ruta actual
- [ ] `ls -la` – Listar archivos con detalles
- [ ] `cd ~/Documents` – Moverte a una carpeta
- [ ] `mkdir prueba-terminal` – Crear carpeta
- [ ] `touch index.html` – Crear archivo vacío
- [ ] `rm index.html` – Eliminar archivo

---

## 🧱 Día 2: Manipulación de archivos y estructura

- [ ] `mv archivo.txt carpeta/` – Mover archivo
- [ ] `cp archivo.txt copia.txt` – Copiar archivo
- [ ] `tree` – Ver estructura (instalar con `brew install tree`)
- [ ] `open .` – Abrir la carpeta actual en Finder

---

## 🔍 Día 3: Búsqueda y lectura

- [ ] `cat archivo.txt` – Leer contenido
- [ ] `bat archivo.txt` – Versión mejorada de `cat` (requiere `brew install bat`)
- [ ] `grep "texto" archivo.txt` – Buscar texto dentro de archivo
- [ ] `find . -name "*.js"` – Buscar archivos por nombre o patrón

---

## 🧠 Día 4: Git básico

- [ ] `git init` – Iniciar repo Git
- [ ] `git status` – Ver cambios
- [ ] `git add archivo.txt` – Añadir archivo al staging
- [ ] `git commit -m "mensaje"` – Commit con mensaje

---

## 🛠️ Día 5: Instalaciones útiles con Homebrew

- [ ] `brew install git`
- [ ] `brew install node`
- [ ] `brew install yarn`
- [ ] `brew install nvm`

---

## 🛠️ Día 6: Aliases y configuración Zsh

- [ ] Editar `~/.zshrc` y agregar:
  ```bash
  alias gs="git status"
  alias ll="ls -la"