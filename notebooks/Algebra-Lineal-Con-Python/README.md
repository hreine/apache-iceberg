<font color='purple' size=2.5><i>Actualizado en agosto de 2025</i></font>
# Clases de Álgebra Lineal

Estas notas de clase están destinadas a cursos introductorios de álgebra lineal, adecuadas para estudiantes universitarios, programadores, analistas de datos, traders algorítmicos, etc.

Las notas de clase se basan libremente en varios libros de texto:

1. <b><i>Linear Algebra and Its Applications</i></b> por Gilbert Strang
2. <b><i>Linear Algebra and Its Applications</i></b> por David Lay
3. <b><i>Introduction to Linear Algebra With Applications</i></b> por DeFranza & Gagliardi
4. <b><i>Linear Algebra With Applications</i></b> por Gareth Williams


Sin embargo, el objetivo principal del curso no es demostrar teoremas, sino mostrar las prácticas y la visualización de los conceptos. Por lo tanto, no nos involucraremos en deducciones o notaciones precisas, sino que nuestro objetivo es aclarar los conceptos esquivos y, gracias a Python/MATLAB, la tarea es mucho más fácil ahora.

## Requisitos previos
Aunque las clases son para principiantes, es beneficioso que los asistentes tengan cierta exposición al álgebra lineal y al cálculo.

Y también se espera que el asistente tenga conocimientos básicos (3 días de capacitación serían suficientes) de
- [x] Python
- [x] NumPy
- [x] Matplotlib
- [x] SymPy

Todos los códigos están escritos de una manera <b>intuitiva</b> en lugar de un estilo de codificación eficiente o profesional, por lo tanto, los códigos son extremadamente sencillos, supongo que casi nadie tendrá dificultades para entender los códigos.

## Configuración del entorno
Uso poetry para la gestión del entorno, si usas VS Code como yo, sigue los pasos a continuación:
1. En Windows Powershell e instala poetry ``` (Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | python -p```
2. Navega a ```cd $env:APPDATA\Python\Scripts```, verifica si poetry está instalado.
3. Abre un bloc de notas ```notepad $profile``` y establece un alias para poetry ```Set-Alias poetry "C:\Users\user\AppData\Roaming\Python\Scripts\poetry.exe"``` en el bloc de notas, prefiero esta forma, porque a veces la configuración de la ruta del entorno no funciona en Windows.
4. Recarga el perfil con ```. $profile```.
5. Si estás en tu computadora personal ```Set-ExecutionPolicy RemoteSigned -Scope CurrentUser``` para relajar tu política de ejecución y elige Y.
6. Restaura la política restringida predeterminada por seguridad ```Set-ExecutionPolicy Restricted -Scope CurrentUser```.
7. Ahora verifica ```poetry --version```, si ves la versión impresa, todo listo.
8. Puedes elegir usar ```poetry update```, o simplemente gestionar la versión a tu conveniencia.

## Qué esperar de las notas
Estas notas te proporcionarán los conocimientos más necesarios y básicos para otras materias, como Ciencia de Datos, Econometría, Estadística Matemática, Ingeniería Financiera, Teoría de Control, etc., que dependen en gran medida del álgebra lineal. Por favor, sigue el tutorial con paciencia, sin duda comprenderás mejor los conceptos fundamentales del álgebra lineal. El siguiente paso es estudiar las matrices especiales y su aplicación con tu conocimiento de dominio.

