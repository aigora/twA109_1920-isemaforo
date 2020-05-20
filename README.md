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
	void funcion_leer(FILE*fentrada)  
	{
	   NODO *lista; // Lista con las URL detectadas
	   //llamar a las funciones de la maquina de estado
	   lista = procesar_fichero (fentrada);
	   fclose (fentrada);
	   imprime_lista(lista);                
	}
   
### Función guardar URLs:	

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
	  NODO * lista_url=NULL;

	  fscanf (fichero,"%c",&letra);
	  while (!feof(fichero))
	  {
	    switch (estado)
	    {
	      case OUT_QUOTES: if (letra == '"') 
			       {
				 estado=IN_QUOTES;  
				 longitud=0;
			       }
			       break;

	      case IN_QUOTES: if (letra!='"')  
			       {
				 cadena[longitud]=letra;  
				 longitud++;
			       }
			       else  
			       {
				 cadena[longitud]='\0';  
				 lista_url= procesa_cadena (cadena,lista_url);
				 estado=OUT_QUOTES; 
			       }
			       break;
	    } 
	   fscanf (fichero,"%c",&letra);
	  } 
	  return lista_url;
	}

### Función procesa cadena (URLs)
	NODO * procesa_cadena (char cadena[],NODO *cabecera)   
	{
	  NODO *p;
	  if (strncmp (cadena,"http",4) == 0)  
	  {
	     p = (NODO *) malloc (sizeof(NODO));  // Se crea un nuevo NODO
	     if (p==NULL)
	       printf ("Memoria insuficiente procesando URLs\n");
	     else
	     {
	       strcpy (p->cadena,cadena);  
	       p->siguiente = cabecera;  
	       cabecera = p;              
	     }
	  }
	  return cabecera;
	}

### Función imprimir URLs
	void imprime_lista (NODO *p) 
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
	void imprime_guardar (NODO *p, FILE *fichero) 
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
	  NODO * lista_imagenes=NULL;  

	  fscanf (fichero,"%c",&letra);
	  while (!feof(fichero))
	  {
	    switch (estado)
	    {
	      case OUT_QUOTES: if (letra == '"') 
			       {
				 estado=IN_QUOTES; 
				 longitud=0;
			       }
			       break;

	      case IN_QUOTES: if (letra!='"')  
			       {
				 cadena[longitud]=letra;  
				 longitud++;
			       }
			       else  
			       {
				 cadena[longitud]='\0';  
				 lista_imagenes= procesa_cadena_imagenes(cadena,lista_imagenes);
				 estado=OUT_QUOTES; 
			       }
			       break;
	    } 
	   fscanf (fichero,"%c",&letra);
	  } 
	  return lista_imagenes;
	}

### Funcion procesar cadena imágenes
	NODO * procesa_cadena_imagenes (char cadena[],NODO *cabecera)
	{
	  NODO *p;
	  if (strncmp (cadena,"images",6) == 0)  
	  {
	     p = (NODO *) malloc (sizeof(NODO));  
	     if (p==NULL)
	       printf ("Memoria insuficiente procesando URLs\n");
	     else
	     {
	       strcpy (p->cadena,cadena);  
	       p->siguiente = cabecera;   
	       cabecera = p;              
	     }
	  }
	  return cabecera;
	}
### Funcion imprimir imágenes
	void imprime_lista_imagenes(NODO *p) 
	{
	  printf ("Imagenes detectadas:\n");
	  while (p!=NULL)
	  {
	    printf ("%s\n",p->cadena);
	    p = p->siguiente;
	  }
	}
