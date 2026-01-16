# Pruebas con clientes en línea de comandos

### Operaciones realizadas con cliente CLI (lftp)

Debido a la configuración de seguridad del servidor (TLS explícito), se utilizó el cliente `lftp` que soporta cifrado moderno, en lugar del cliente `ftp` básico.

### Pasos

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasConClientesEnL-neaDeComandos/refs/heads/main/1.png)

| Comando | Función |
| :--- | :--- |
| `lftp` | Inicia el programa cliente FTP avanzado. |
| `set ssl:verify-certificate no` | Configuración crítica: instruye al cliente para que confíe en el certificado "autofirmado" del servidor y no corte la conexión por seguridad. |
| `open -u tester,tester 127.0.0.1` | Abre la conexión al servidor (IP 127.0.0.1) autenticándose directamente con usuario y contraseña. |
| `ls` | **Listar.** Muestra el contenido del directorio remoto (en este caso `/tmp/ftp_lab`). |
| `put archivo_local.txt` | **Subir.** Transfiere un archivo desde el cliente al servidor. |
| `get archivo_del_servidor.txt` | **Descargar.** Transfiere un archivo desde el servidor hacia el cliente. |
| `exit` | Cierra la sesión y el programa. |
