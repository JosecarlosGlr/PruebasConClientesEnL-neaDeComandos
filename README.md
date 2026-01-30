# Pruebas con clientes en línea de comandos

### Operaciones realizadas con cliente CLI (lftp)

Debido a la configuración de seguridad del servidor (TLS explícito), se ha utilizado el cliente `lftp`. A diferencia del cliente `ftp` básico, `lftp` permite gestionar conexiones cifradas de forma nativa, lo cual es imprescindible dado que el servidor requiere explícitamente FTP sobre TLS.

---

### Pasos y Evidencias

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasConClientesEnL-neaDeComandos/refs/heads/main/1.png)
**Preparación del entorno:** He generado un archivo de prueba local mediante el comando `echo "Prueba de FTP" > prueba.txt` y he verificado la instalación del cliente `ftp` estándar.

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasConClientesEnL-neaDeComandos/refs/heads/main/2.png)
**Instalación de lftp:** He instalado el paquete `lftp` mediante `sudo apt install lftp` y realizado una primera prueba de conexión con el `Usuario1` para verificar la visibilidad del servidor en la dirección local.

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasConClientesEnL-neaDeComandos/refs/heads/main/4.png)
**Gestión de Usuarios:** Muestro la configuración del servidor donde se aprecia el usuario **"tester"**. Este usuario tiene acceso de lectura y escritura (`Read + Write`) sobre el directorio raíz, lo que permite realizar pruebas completas de transferencia.

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasConClientesEnL-neaDeComandos/refs/heads/main/3.png)
**Conexión y Listado:** Tras iniciar `lftp` y desactivar la verificación estricta de certificados, he abierto la sesión con el usuario `tester`. El comando `ls` confirma la presencia del archivo `archivo_del_servidor.txt` en el servidor.

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasConClientesEnL-neaDeComandos/refs/heads/main/5.png)
**Transferencia de archivos:** He realizado el ciclo completo de transferencia:
1. He creado un nuevo archivo local.
2. He utilizado `put` para subirlo al servidor.
3. He utilizado `get` para descargar el archivo original del servidor.
4. Mediante `!ls`, he verificado que ambos archivos se encuentran ahora en mi directorio local.

---

### Resumen de comandos utilizados

| Comando | Función |
| :--- | :--- |
| `lftp` | Inicia el intérprete del cliente FTP avanzado. |
| `set ssl:verify-certificate no` | Permite la conexión omitiendo la validación de la CA (necesario para certificados autofirmados). |
| `open -u tester,tester 127.0.0.1` | Conecta al servidor local usando las credenciales del usuario `tester`. |
| `ls` | **Listar:** Muestra los archivos disponibles en el directorio remoto del servidor. |
| `put archivo_local.txt` | **Subir:** Envía el archivo indicado desde el PC local hacia el servidor FTP. |
| `get archivo_del_servidor.txt` | **Descargar:** Trae el archivo indicado desde el servidor hacia el equipo local. |
| `!ls` | Ejecuta el comando `ls` en el sistema local sin salir de la sesión de `lftp`. |
