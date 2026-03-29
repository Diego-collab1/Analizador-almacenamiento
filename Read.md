# Analizador de Almacenamiento

Esta herramienta desarrollada en Python permite realizar un escaneo profundo de directorios para identificar archivos y carpetas que consumen espacio excesivo en el disco duro. Es especialmente útil para entornos de desarrollo donde archivos temporales o configuraciones de Git incorrectas pueden saturar el almacenamiento.

## Uso del Comando

El script acepta una ruta como argumento. Por defecto, se puede utilizar el símbolo de tilde `~` para representar el directorio raíz del usuario en sistemas macOS y Linux.

### Comando base:
./almacenamiento ~

### Análisis de subdirectorios:
Para analizar una ruta específica dentro de su estructura de archivos, añada la ubicación después del símbolo de usuario.

Ejemplo:
./almacenamiento ~/Documents/Proyectos/Laravel

---

## Instalación Global (Opcional)

Si deseas poder ejecutar el comando `almacenamiento` desde cualquier carpeta de tu terminal sin necesidad de usar `./` ni tener que estar posicionado en el directorio del proyecto, puedes configurar un "alias" en tu sistema.

Para usuarios de Mac/Linux que utilicen `zsh` (por defecto en macOS actual), puedes ejecutar esto en tu terminal una única vez:

```bash
echo '\nalias almacenamiento="'$PWD'/almacenamiento"' >> ~/.zshrc
source ~/.zshrc
```

*(Si lo moviste a otra carpeta, asegúrate de reemplazar `'$PWD'` con la ruta absoluta de la carpeta donde clonaste el proyecto).*

A partir de entonces, podrás usar el sistema desde cualquier lugar simplemente escribiendo:

```bash
almacenamiento ~
```

---

## Detección de Directorios .git de Gran Tamaño

Un problema común en el desarrollo es la creación accidental de repositorios Git en directorios raíz (como /Users/nombre-usuario), lo que genera un "Git Fantasma".

### Diferenciación técnica:
1. Repositorio de Proyecto: Ubicado dentro de la carpeta del código fuente. Su tamaño suele ser proporcional al código y activos del proyecto (pocos MB).
2. Repositorio Accidental: Ubicado en la raíz del sistema o usuario. Puede alcanzar tamaños superiores a 40 GB ya que Git intenta indexar archivos del sistema, descargas y multimedia.

### Resolución de conflictos:
Si el análisis identifica una carpeta .git con un tamaño injustificado, verifique su ubicación con el comando `pwd`. Si se encuentra en una ruta incorrecta, puede eliminar la base de datos de Git sin afectar sus archivos personales mediante:
rm -rf /ruta/detectada/.git