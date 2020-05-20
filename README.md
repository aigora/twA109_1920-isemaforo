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
    printf("1.Leer\n");
    printf("2.Guardar\n");
    printf("3.Imagenes\n");
    printf("4.Salir\n");
    scanf("%d",&opcion);
    }
    while((opcion<1) || (opcion>4));
    
 return opcion;
 }
 
### Función Leer URLs:
	//Abrir página html y mostrar enlaces existentes.
	
void funcion_leer(FILE*fentrada)   // buscar enlaces
{
    
    NODO *lista; // Lista con las URL detectadas
    
    //llamar a las funciones de la maquina de estado
    lista = procesar_fichero (fentrada);
    fclose (fentrada);
    imprime_lista(lista);                
}
   
### Función guardar URLs:
	//Almacenar en un fichero los enlaces detectados por la función abrir.
	
FILE* funcion_guardar(FILE *entrada) //guarda todas las urls encontradas en un fichero nuevo
{
    FILE *nuevo;
    int cierre;
    NODO *lista_guardar;
    
    lista_guardar = procesar_fichero (entrada);
    fclose (entrada);
    
    
    nuevo = fopen("Encontradas.txt","w");
    
    if(nuevo==NULL)
        printf("No se ha podido abrir el fichero\n");
    else
    {
        
        imprime_guardar(lista_guardar,nuevo);
        fclose(nuevo);
        
        if(cierre == EOF)
            printf("No se ha podido cerrar el fichero\n");
        else
            printf("Fichero creado\n");
    }
    return nuevo;
}

###  Función ver imágenes:
	Identificar qué enlaces de los anteriores son imágenes y mostrar las mismas en pantalla.
void funcion_imagenes(FILE *fichero)
{
    NODO *lista_imagenes;
    
    lista_imagenes = procesar_fichero_imagenes (fichero);
    fclose (fichero);
    imprime_lista_imagenes(lista_imagenes);
}

### Función procesar fichero (URLs)
NODO * procesar_fichero(FILE *fichero)
{
  char letra;
  int estado=OUT_QUOTES;
  char cadena[L],longitud;
  NODO * lista_url=NULL;  // Inicialmente la lista de Urls esta vacia
  
  fscanf (fichero,"%c",&letra);
  while (!feof(fichero))
  {
    switch (estado)
    {
      case OUT_QUOTES: if (letra == '"') // Si estando fuera aparecen comillas
                       {
                         estado=IN_QUOTES;  // Cambiamos de estado
                         longitud=0;
                       }
                       break;

      case IN_QUOTES: if (letra!='"')  // Si estando dentro aparece un caracter diferente a comillas
                       {
                         cadena[longitud]=letra;  // Se almacena en la cadena
                         longitud++;
                       }
                       else  // Si aparecen comillas se interpretan como comillas de cierre
                       {
                         cadena[longitud]='\0';  // Se cierra la cadena y se procesa
                         lista_url= procesa_cadena (cadena,lista_url);
                         estado=OUT_QUOTES; // Y cambia de estado
                       }
                       break;
    } // Fin del switch
   fscanf (fichero,"%c",&letra);
  } // Fin del while
  return lista_url;
}

### Función procesa cadena (URLs)
NODO * procesa_cadena (char cadena[],NODO *cabecera)   // Recibe una cadena y un enlace a una lista de NODO
{
  NODO *p;
  if (strncmp (cadena,"http",4) == 0)  // Si la cadena comienza por http se considera una URL
  {
     p = (NODO *) malloc (sizeof(NODO));  // Se crea un nuevo NODO
     if (p==NULL)
       printf ("Memoria insuficiente procesando URLs\n");
     else
     {
       strcpy (p->cadena,cadena);  // Se copia la cadena en el nuevo NODO
       p->siguiente = cabecera;   // Se enlaza el nuevo NODO con el principio de la lista
       cabecera = p;              // Se apunta el inicio de la lista al nuevo NODO
     }
  }
  return cabecera;
}

### Función imprimir URLs
void imprime_lista (NODO *p) // Recorre una lista de NODO e imprime las URL
{
    
  printf ("URLs detectadas:\n");
  while (p!=NULL)
  {
    printf ("%s\n",p->cadena);
    p = p->siguiente;
  }
  
  return ;
}

### Función crear fichero con las URLs
void imprime_guardar (NODO *p, FILE *fichero) // Recorre una lista de NODO e imprime las URL
{
    
  
  while (p!=NULL)
  {
    fprintf(fichero,"%s\n",p->cadena);
    p = p->siguiente;
  }
  
  return ;
}

### Función procesar fichero imágenes
NODO * procesar_fichero_imagenes(FILE *fichero)
{
  char letra;
  int estado=OUT_QUOTES;
  char cadena[L],longitud;
  NODO * lista_imagenes=NULL;  // Inicialmente la lista de Urls esta vacia
  
  fscanf (fichero,"%c",&letra);
  while (!feof(fichero))
  {
    switch (estado)
    {
      case OUT_QUOTES: if (letra == '"') // Si estando fuera aparecen comillas
                       {
                         estado=IN_QUOTES;  // Cambiamos de estado
                         longitud=0;
                       }
                       break;

      case IN_QUOTES: if (letra!='"')  // Si estando dentro aparece un caracter diferente a comillas
                       {
                         cadena[longitud]=letra;  // Se almacena en la cadena
                         longitud++;
                       }
                       else  // Si aparecen comillas se interpretan como comillas de cierre
                       {
                         cadena[longitud]='\0';  // Se cierra la cadena y se procesa
                         lista_imagenes= procesa_cadena_imagenes(cadena,lista_imagenes);
                         estado=OUT_QUOTES; // Y cambia de estado
                       }
                       break;
    } // Fin del switch
   fscanf (fichero,"%c",&letra);
  } // Fin del while
  return lista_imagenes;
}

### Funcion procesar cadena imágenes
NODO * procesa_cadena_imagenes (char cadena[],NODO *cabecera)
{
  NODO *p;
  if (strncmp (cadena,"images",6) == 0)  // Si la cadena comienza por images se considera una imagen
  {
     p = (NODO *) malloc (sizeof(NODO));  // Se crea un nuevo NODO
     if (p==NULL)
       printf ("Memoria insuficiente procesando URLs\n");
     else
     {
       strcpy (p->cadena,cadena);  // Se copia la cadena en el nuevo NODO
       p->siguiente = cabecera;   // Se enlaza el nuevo NODO con el principio de la lista
       cabecera = p;              // Se apunta el inicio de la lista al nuevo NODO
     }
  }
  return cabecera;
}
### Funcion imprimir imágenes
void imprime_lista_imagenes(NODO *p) // Recorre una lista de NODO e imprime las imagenes
{
  printf ("Imagenes detectadas:\n");
  while (p!=NULL)
  {
    printf ("%s\n",p->cadena);
    p = p->siguiente;
  }
}

