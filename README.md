# My Development Setup

Este documento describe cómo configuré mi entorno de desarrollo en Ubuntu y macOS. Es solo una guia personal para cuando necesito recordar algo. Intento mantenerla actualizada constantemente y espero le resulte útil a alguien más.

**Contribución**: Si encuentra algún error en los pasos descritos a continuación, o si alguno de los comandos no está actualizado, ¡hágamelo saber!.

- [Preferencias](#preferencias)
- [Terminal](#Terminal)
- [Git](#git)
- [Zsh](#zsh)
- [Node.js](#node.js)
- [Mobile Frameworks](#mobile-frameworks)
- [OpenJDK](#openjdk)
- [Gradle](#gradle)
- [Netbeans IDE](#netbeans-ide)
- [Android Studio](#android-studio)
- [Projects folder](#projects-folder)


## Preferencias

Lo primero que debe hacer, en cualquier sistema operativo, ¡es actualizar el sistema!

**macOS:** *Icono de Apple > Acerca de esta Mac* y luego *Actualización de software*.

**ubuntu:** `sudo apt update && sudo apt upgrade -y`


## Terminal

Fuentes Fira (Code, Mono y Sans) desde [Google Fonts](https://fonts.google.com/?query=fira)

*Columnas 120 > Filas 35 > Fira Mono 11 > Esquema de color OneDark*

Checkear esto https://github.com/Mayccoll/Gogh


### Git

**En macOS**

- instalamos primero [Homebrew](http://brew.sh/)
- luego *Git* > `brew install curl git`

On a Mac, it is important to remember to add `.DS_Store` (a hidden macOS system file that's put in folders) to your project `.gitignore` files. You also set up a global `.gitignore` file, located for instance in your home directory (but you'll want to make sure any collaborators also do it):

```
cd ~
curl -O https://raw.githubusercontent.com/ctrbts/my-dev-setup/master/.gitignore
git config --global core.excludesfile ~/.gitignore
```

### Zsh

Ahora vamos a agregar ZSH y OhMyZsh siguiendo [esta guía][instalar zsh]:

- Para instalarlo: `sudo apt install curl git zsh -y`
- Para poner ZSH como shell por defecto: `chsh -s $(which zsh)`, (en macOS es importante hacer el cambio por la versión instalada desde `brew install zsh` con `chsh -s /usr/local/bin/zsh`)

Luego cerrar sesión y volver a entrar. Cuando iniciemps por primera vez la terminal nos va a preguntar por el archivo de configuración, elegimo la opción 0 y continuamos.

[Oh My ZSH][omz] es un framework con una gran comunidad detrás con muchos temas y plugins para añadir funcionalidad a ZSH.

Para instalarlo: `sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`

OhMyZsh tiene muchos plugins, los que mas uso son:

**git** que viene instalado por defecto y añade un montón de alias de git **common-aliases** Añade ciertos alias interesantes, entre ellos: G para añadir | grep al final de un comando

**colored-man** colorea las páginas del manual.

**extract** permite descomprimir cualquier tipo de archivo comprimido de una forma común: `x nombre-fichero-comprimido`

**zsh-autosuggestions** este plugin busca en el historial tus últimos comandos y te va autocompletando los mismos.

Para instalarlo: `git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions`

**zsh-syntax-highlighting** este plugin colorea los comandos en verde o en rojo dependiendo de si son correctos o no.

Para instalarlo: `git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting`

Para activarlos hay que modificar el fichero de configuración *~/.zshrc*:

```
plugins=(
  git
  common-aliases
  extract
  colored-man-pages
  zsh-autosuggestions
  zsh-syntax-highlighting
)
```

## Node.js

La manera recomendada para instalar [Node.js](http://nodejs.org/) es con [nvm](https://github.com/creationix/nvm) (Node Version Manager) que nos permite administrar multiples versiones de Node.js en la misma máquina.

Para instalar `nvm` copiamos y pegamos el [install script command](https://github.com/creationix/nvm#install--update-script) en la terminal.

Reiniciamos la terminal y comprobamos se ejecute correctamente con `command -v nvm`

Ahora verificamos las versiones dispinibles de Node `nvm ls-remote --lts`

Instalamos la última LTS `nvm install --lts` o alguna versión específica `nvm install 11.15.0`

El resto de los comandos estan disponibles desde el repositorio de NVM


## Mobile Frameworks

`npm i -g cordova framework7-cli @ionic/cli`


## OpenJDK

Instalamos el ***JDK*** desde https://adoptopenjdk.net/installation.html#installers

**En ubuntu** > Import the official AdoptOpenJDK GPG key by running the following command: `wget -qO - https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public | sudo apt-key add -` > then > Import the AdoptOpenJDK DEB repository by running the following command:
```
sudo apt-get install -y software-properties-common
sudo add-apt-repository --yes https://adoptopenjdk.jfrog.io/adoptopenjdk/deb/
```
Refresh your package list with sudo apt-get update and then install your chosen AdoptOpenJDK package. For example, to install OpenJDK 8 with the HotSpot VM, run: `sudo apt-get install adoptopenjdk-8-hotspot`

**En macOS** > `brew cask install adoptopenjdk/openjdk/adoptopenjdk8`

## Gradle

**En ubuntu** > descargamos el binario desde https://gradle.org/next-steps/?version=6.6.1&format=bin > creamos el directorio con `sudo mkdir /opt/gradle` y descomprimimos con `sudo unzip -d /opt/gradle gradle-6.6.1-bin.zip`

**En macOS** > `brew install watchman gradle`

#### Add the following lines to your ~/.zshrc) config file:
```
export GRADLE_HOME=/opt/gradle/gradle-6.6.1 (ubuntu)
export GRADLE_HOME=/usr/local/Cellar/gradle/6.6.1 (macOS)
export PATH=$PATH:$GRADLE_HOME/bin
```
## Netbeans IDE

Development Environment, Tooling Platform and Application Framework.
To download > https://netbeans.apache.org/download/index.html


## Android Studio

Select the "SDK Platforms" tab from within the SDK Manager, then check the box next to "Show Package Details" in the bottom right corner. Look for and expand the Android 10 (Q) entry, then make sure the following items are checked:

- Android SDK Platform 29
- Intel x86 Atom_64 System Image or Google APIs Intel x86 Atom System Image

Next, select the "SDK Tools" tab and check the box next to "Show Package Details" here as well. Look for and expand the **Android SDK Build-Tools** entry, then make sure that **29.0.2** is selected.

Finally, click "Apply" to download and install the Android SDK and related build tools.

#### Add the following lines to your ~/.zshrc) config file:
```
export ANDROID_HOME=$HOME/android-sdk (ubuntu)
export ANDROID_HOME=$HOME/Library/Android/sdk (macOS)

export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools
```

## Apps
brew cask install dbeaver-community
brew cask install superproductivity

## Projects folder

Esto realmente depende de cómo quieras organizar tus archivos, pero me gusta poner todos mis proyectos controlados por versión en `~/Proyectos`. Otros documentos que pueda tener, o cosas que aún no están bajo control de versión, me gusta tenerlas sincronizadas desde Google Drive.


## Referencias

[instalar zsh]: https://www.asanzdiego.com/2018/04/instalar-y-configurar-zsh-y-ohmyzsh-en-ubuntu.html
[omz]: https://ohmyz.sh/
