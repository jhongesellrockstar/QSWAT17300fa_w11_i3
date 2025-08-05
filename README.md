# QSWAT17300fa_w11_i3
Este es un proyecto que contiene recién el código en la primera carpeta llamada QSWATPlus-master; me interesa el código de su interior ya que intento compilarlo, su Makefile está en `C:\Users\user\Documents\QSWATPlus-master\QSWATPlus` de esta computadora en la que me limito a trabar allí.

## Compilación con Python 3.12
Antes de ejecutar `make` es necesario preparar el entorno de Python:

1. Definir `PYTHONHOME=C:/OSGeo4W/apps/Python312`.
2. Cambiar (`cd`) a un directorio que no contenga las carpetas `Lib` ni `site-packages` antes de invocar cualquier comando de Python.
3. Desde ese directorio comprobar que el intérprete funciona:

   ```bash
   python3.exe -c "import encodings"
   ```

Estos pasos evitan que Python cargue módulos erróneos durante la compilación.
