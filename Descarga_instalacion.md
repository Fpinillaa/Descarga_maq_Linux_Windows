# Selección de máquina virtual

La selección y descarga de nuestra máquina virtual de Ubuntu la realizaremos directamente desde Microsoft Store, el cual se encuentra instalado en nuestras máquinas con Windows, por lo que solo necesitaremos abrirlo.

![Microsoft Store](Image_Linux_Windows/busqueda_Linux.png)

Luego de abrir Microsoft Store, en la barra de búsqueda escribiremos Ubuntu y seleccionaremos la primera opción que aparece, que es de **Canonical Group Limited**. Al seleccionar la máquina virtual, la página se recargará brevemente y, en la esquina superior derecha, veremos un recuadro que dirá Obtener. Hacemos clic en este recuadro y comenzará la descarga de la máquina virtual.

![Microsoft Store Descarga](Image_Linux_Windows/Selección_del_sistema2.png)

# Instalación de WSL

Mientras se descarga la máquina virtual, comenzaremos con la instalación de `WSL`, que es el programa que permite la comunicación entre la máquina virtual y Windows. Para instalarlo, debemos buscar PowerShell en el buscador de Windows y ejecutarlo como administrador.

![PowerShell](Image_Linux_Windows/Powershell1.png)

Al abrir PowerShell, se desplegará una ventana solicitando permisos de administrador. Aceptamos, y se abrirá la terminal del sistema Windows, donde deberemos escribir el siguiente comando para instalar WSL:

````bash
wsl --install
````

![PowerShell2](Image_Linux_Windows/PowerShell21.png)

Una vez finalizada la instalación de WSL, es muy probable que la máquina virtual de Ubuntu ya se haya descargado. Sin embargo, **¡OJO!**, aún no debemos abrir Ubuntu. Antes de hacerlo, es necesario reiniciar el equipo para que se complete correctamente la instalación de WSL.

Finalmente, después del reinicio, podremos abrir Ubuntu. Este nos pedirá ingresar un nombre de usuario y, posteriormente, una clave. Importante: el nombre de usuario puede ser cualquiera; no es necesario que coincida con el nombre del equipo. Lo más importante es el ingreso de la clave. **Al escribirla, no se verá en pantalla, y el sistema no mostrará ningún indicador de que se está escribiendo, por lo que se recomienda:**

1. Tener clara la clave que se va a utilizar.

2. No olvidarla y mantenerla anotada en un lugar seguro pero no fácilmente accesible.

Esto es crucial, ya que en algunos casos se requerirá forzar instalaciones o modificar archivos del sistema, y Ubuntu pedirá esta clave para realizar dichos cambios.

# Uso de Shell/bash

## Comandos básicos 

- `cd`: Cambiar de directorio. Permite moverse entre carpetas. Se usa con `../` para retroceder y con `nombre_carpeta/` para ingresar a una carpeta específica.
- `ls`: Listar archivos. Muestra los diferentes archivos que hay en un directorio.
- `rm`: Eliminar archivos. Usar con cuidado. Para eliminar directorios, se debe usar con la opción `-r`.
- `cat`: Imprime archivos de texto en la terminal.
- `nano`: Editor de texto. Permite modificar archivos directamente desde la terminal. (Nota: dentro de nano, solo puedes moverte con las flechas del teclado. Para salir, presiona `Ctrl + X`; si no deseas cambiar el nombre del archivo, simplemente presiona Enter para guardar).
- `head`: Muestra las primeras líneas de un archivo de texto. Con la opción `-n` puedes especificar cuántas líneas deseas ver. Ejemplo: `head -n 10 archivo.txt` muestra las primeras 10 líneas.
- `tail`: Similar a head, pero muestra las últimas líneas del archivo. También se puede usar con `-n`.

Estos son los comandos principales que se utilizan al comenzar. Si se requiere más información sobre los comandos o sus opciones, se puede usar el comando correspondiente seguido de la opción `-h` o `--help`, lo cual mostrará en la terminal las distintas opciones y su sintaxis.

# Instalación de Conda

Conda es un gestor de ambientes, los ambientes son entornos virtuales que permiten gestionar de forma independiente los paquetes que uno descargue en esos ambientes, paquetes que poseen funciones para el análisis de secuencias genéticas.

````bash
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
````

Finalizada la instalación deberemos reiniciar la consola (cerrar y abrir de nuevo Ubuntu) para que se finalice la instalación.
Para corroborar que esté instalado debemos ocupar el siguiente código `conda --version` que nos deberá entregar la versión de conda instalada en nuestro sistema.

Luego de corroborar que esta conda instalado, podremos crear ambientes y activarlos, para poder descargar los paquetes que vayamos a utilizar en ese ambiente.

**Creación de ambiente**
````bash
conda create -n <nombre_ambiente>
````

**Activación del ambiente**
````bash
conda activate <nombre_ambiente>
````

**Descarga paquete**
En este punto hay que estar atento: 
1) Cuando instalas un paquete con una ambiente activado, este paquete quedara en ese ambiente alojado, por lo que si quieres ocupar su función, tendrás que activar el ambiente para poder hacerlo.
2)  Dependiendo del paquete este se instalara directamente por conda o bien se necesitara instalar por bioconda de la siguiente manera
````bash
#conda directamente
conda install <nombre_del_paquete>

#bioconda
conda install -c bioconda <nombre_del_paquete>
````
> Se sugiere saber de ante mano como se instala el paquete o bien probar con uno de los dos métodos mencionados anteriormente

**Desactivar el ambiente**
````bash
conda deactivate
````

Con esto ya debería quedar funcionando de buena manera la máquina virtual de Ubuntu y Conda para realizar los análisis :D.

