# HTML Links
Es una aplicación que parte de un fichero de texto que en realidad es una página en html, el programa identifica los enlaces que tiene y almacena la relación de enlaces en otro fichero de texto.

El programa tiene un menú de opciones:

1º Abrir página html y mostrar enlaces existentes
2º Almacenar en un fichero los enlaces detectados por la opción 1
3º Identificar qué enlaces de los anteriores son imágenes y mostrar las mismas en pantalla.
4º Finalizar el programa

## Integrantes del equipo
Guillermo Martín Lechuga 54727
Noelia López Rúa 54705

## Objetivos del trabajo
Crear una aplicación que partiendo de un fichero de texto (html) indentifique los enlaces que hay en él y almacene la relación de enlaces en otro fichero de texto.

Anprender a usar lenguaje hmtl.
Usar ficheros.

## Subprogramas (funciones)

### Función menú:
	En esta función se procesará la opción elegida por el usuario.
  
	int menu()
	{
	 int opcion;
	 do
	 {
		printf("Menu:\n");
		print("1.Abrir\n");
	    	printf("2.Guardar\n");
		printf("3.Ver\n");
	    	printf("4.Salir\n");
		scanf ("%d",&opcion);
	   } 
	   while ((opcion<1) || (opcion>4)); 
 	return opcion;
 	}
 
### Función abrir:
	Abrir página html y mostrar enlaces existentes.
   
### Función guardar:
	Almacenar en un fichero los enlaces detectados por la función abrir.

###  Función ver:
	Identificar qué enlaces de los anteriores son imágenes y mostrar las mismas en pantalla.
