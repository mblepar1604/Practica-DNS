PASO 1: Creación de la estructura de las máquinas virtuales + ip --SIN PROVISIONS--

He creado la estructura principal de las máquinas virtuales y les he puesto la ip correspondiente a cada una
![alt text](img/image1.png)

------------------------------------------------------------------------------------

PASO 2: Instalación de bind9 y copia de sus archivos a modificar en mi repositorio

He añadido la provision de bind9 en el codigo y he copiado los archivos a modificar en una carpeta "files"
![alt text](img/image2.png)

------------------------------------------------------------------------------------

PASO 3: Modificación de los archivos de configuración para que:
    - El servidor solo escuche al protocolo IPv4.
    ![alt text](img/image3-1.png)

    - Se establezca la opción de dnssec-validation a yes.
    - Los servidores permitan las consultas recursivas a solamente a los ordenadores de la red 127.0.0.0/8 y en la red 192.168.57.0/24 usando la opción acl.
    ![alt text](img/image3-2.png)

    - El servidor maestro sea tierra.sistema.test y tenga autoridad sobre la zona directa e inversa.
    ![alt text](img/image3-3.png)
    ![alt text](img/image3-4.png)
    ![alt text](img/image3-5.png)

    - El servidor esclavo sea venus.sistema.test y su maestro sea tierra.sistema.test.
    ![alt text](img/image3-6.png)

------------------------------------------------------------------------------------

PASO 4: Segunda modificación de archivos de configuración para que:
    - El tiempo de caché de las respuestas negativas sea de 2 horas.
    - Las consultas no autorizadas sean reenviadas al servidor de OpenDNS
    - Se configuren los alias:
        · ns1.sistema.test para tierra
        · ns2.sistema.test para venus
        · mail.sistema.test para marte
    - El equipo de marte.sistema.test actue como servidor de correo del dominio
    - Reajustes varios en archivos que podrían dar error

    ![alt text](img/image4-1.png)
    ![alt text](img/image4-2.png)