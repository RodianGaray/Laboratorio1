# LABORATORIO 1 — Memorias booteables con Rufus y Ventoy

**Objetivo:** Crear memorias USB booteables con Rufus y Ventoy, documentar el proceso (descarga, verificación, creación, instalación de Ubuntu) y entregar un README en Markdown listo para subir a GitHub. Las imágenes de cada paso se colocan en la carpeta `images/` y se enlazan en este README.

---

## Punto 1 — Rufus y Ventoy en memorias separadas

### 1.1 Explicar el proceso de Booteo (Rufus y Ventoy)

* **Rufus:** Graba la ISO directamente en la memoria USB. Al arrancar, la BIOS/UEFI reconoce el sistema de arranque escrito y carga el instalador de Ubuntu.  

* **Ventoy:** Instala un gestor propio en la USB. Luego, al arrancar, muestra un menú con todas las ISOs copiadas en la memoria, permitiendo seleccionar cuál usar.  

### 1.2 ¿Para qué sirve un bootloader y qué es GRUB?

* **Bootloader:** Es el programa que inicializa el sistema operativo desde un disco o memoria booteable. Permite cargar el kernel y pasarle parámetros.
* **GRUB (GNU GRUB):** Es el bootloader más común en Linux. Ofrece un menú de selección de sistemas operativos y configuraciones avanzadas de arranque.  

### 1.3 Sistemas de archivos compatibles

* **FAT32:** Alta compatibilidad (UEFI), pero no admite archivos >4 GB.  
* **NTFS:** Propio de Windows, útil cuando la ISO contiene archivos grandes.  
* **exFAT:** Similar a FAT32 pero con soporte de archivos grandes, compatible con Ventoy.  
* **ext4:** Nativo de Linux, usado en instalaciones finales, no en ISOs booteables.  

### 1.4 Estructura de particiones

* **Definición:** División lógica de un disco físico para organizar datos y sistemas.
* **Tipos:**

  * **MBR (Master Boot Record):** Antiguo, soporta hasta 2 TB y 4 particiones primarias.  
  * **GPT (GUID Partition Table):** Moderno, soporta discos grandes y múltiples particiones, requerido por UEFI.  

---

## Punto 2 — Descarga de imágenes de Ubuntu y Windows

### 2.1 Imagen de Ubuntu en memoria con Rufus

1. Descargar la ISO oficial de Ubuntu.  
   ![Seleccionar Ubuntu](Laboratorio1/Selecciona_ubuntu.JPG)
2. Insertar la memoria USB.  
   ![Abrir Rufus](images/Abrir_rufus.png)
3. Abrir Rufus → seleccionar dispositivo.  
4. Elegir la ISO → esquema de partición GPT o MBR según el sistema.  
5. Seleccionar sistema de archivos FAT32.  
6. Iniciar el proceso (`START`).  

### 2.2 Imagen de Ubuntu y Windows en memoria con Ventoy

1. Descargar las ISOs oficiales (Ubuntu + Windows).  
2. Instalar Ventoy en la memoria USB (borra todos los datos).  
   ![Ventoy instalación](images/03_ventoy_install.png)  
3. Copiar las ISOs directamente a la memoria (sin extraer).  
   ![Ventoy copiar ISOs](images/04_ventoy_copied_isos.png)  
4. Al arrancar, Ventoy mostrará un menú para seleccionar la ISO.  

---

## Punto 3 — Uso de la memoria booteable e instalación de Ubuntu

### 3.1 Arrancar desde la USB

1. Encender el PC y abrir menú de arranque (teclas típicas: F12, ESC, F10).  
2. Seleccionar la USB creada con Rufus o Ventoy.  
   ![Boot menu](images/05_boot_menu.png)  

### 3.2 Instalación paso a paso de Ubuntu

1. Seleccionar idioma: Español.  
   ![Idioma](images/06_ubuntu_lang.png)  
2. Elegir `Install Ubuntu`.  
   ![Iniciar instalación](images/07_install_start.png)  
3. Preparación de instalación: normal o mínima + drivers.  
   ![Opciones instalación](images/08_install_options.png)  
4. Tipo de instalación: borrar disco, instalar junto a Windows o *Algo más*.  

### 3.3 Particionado manual (opción *Algo más*)

* **/boot/efi (ESP):** 512 MB, FAT32, punto `/boot/efi`.  
* **/** (raíz): 40 GB, ext4, punto `/`.  
* **/home:** resto, ext4, punto `/home`.  
* **swap:** opcional, tamaño ≈ RAM.  
  ![Particiones](images/09_partition_table.png)  

### 3.4 Proceso de instalación

1. Confirmar cambios y proceder.  
2. Configurar zona horaria, teclado, usuario.  
3. Esperar finalización.  
   ![Progreso instalación](images/10_install_progress.png)  
   ![Instalación completa](images/11_install_complete.png)  

### 3.5 Primer arranque

1. Retirar la USB y reiniciar.  
2. GRUB mostrará Ubuntu (y Windows si hay dual-boot).  
   ![Primer arranque](images/12_first_boot.png)  

---

## Conclusión

Con este laboratorio se logró:

* Crear una memoria booteable con Rufus (Ubuntu).
* Crear una memoria multi-ISO con Ventoy (Ubuntu + Windows).
* Instalar Ubuntu paso a paso, incluyendo particionado manual.
* Documentar todo en Markdown, con capturas.
