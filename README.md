# LibrarySqLite
libreria Android para usar las funciones de base de datos en el celular.

1) Crear el modelo de base de datos:

        TablaDto tablaDto = new TablaDto();
        tablaDto.setNombreTabla("WISROVI");
        List<ColumnasDto> columnasDtos = new ArrayList<>();
        columnasDtos.add(new ColumnasDto("nombre", TiposDatoSqLite.DatoString));
        columnasDtos.add(new ColumnasDto("documento", TiposDatoSqLite.DatoEntero));
        columnasDtos.add(new ColumnasDto("habilitado", TiposDatoSqLite.DatoBoolean));
        tablaDto.setColumnasDtos(columnasDtos);
        
2)  Conectar el modelo con una conexion estable de SqLite:

        ConectarSqLite conectarSqLite = new ConectarSqLite(MainActivity.this, tablaDto);
        
3) Obtener una platilla modificable para llenar nuevos datos, se usa esta plantilla para insertar nuevos datos o actualizar datos existentes

            List<DatosColumnasDto> datosColumnasDtos = conectarSqLite.plantillaUsoDatos();
            
4) Preparando datos para insertar o editar:

  En el ejemplo del punto 1) se ha creado una tabla llamada: WISROVI
  con tres columnas:
    > nombre (tipo String) --------------> columna 0
    > documento (tipo entero) -----------> columna 1
    > habilitado (tipo boolean) ---------> columna 2

  para editar usarmos el datosColumnasDtos y reemplazamos segun el numero de la columna
  
          List<DatosColumnasDto> datosColumnasDtos = conectarSqLite.plantillaUsoDatos();
          datosColumnasDtos.get(0).setDatoColumna("William");
          datosColumnasDtos.get(1).setDatoColumna(Integer.toString(123456));
          datosColumnasDtos.get(2).setDatoColumna(Boolean.toString(false));
                                °
                                |
                                |
                            numero de la columna a insertar el dato, es necesario tener presente esta numero para enviar un dato correcto segun se estipulo en la creacion de la tabla, ver punto 1)
          
  con esto ya tenemos los datos preparados para insertar o actualizar
  
5) Insertar datos:

  para insertar datos usamos la instruccion:
  
          int aLong = conectarSqLite.InsertarDatos(datosColumnasDtos);
          
  esta insercion me devuelve un entero, generalmente devuelve el id de la fila donde se inserto el dato, pero si se presenta un error, dara como resultado un valor negativo que podemos filtrar.
  
        switch (aLong){
            case 0:{
                //no se pudo insertar
            }break;
            case -1:{
                //"Datos incompletos para ser guardados", faltan datos para insertar en la fila
            }break;
            case -2:{
                //error procesar datos, es posible que un dato se haya enviado en un formato incorrecto, por ejemplo, para insertar un                   //boolean envie un String y en la conversion el sistema detecto un error, por eso es importante conocer el id de columna
            }break;
        }
          
          
6) Actualizar dato:
    Para este existe el comando:
    
         List<DatosColumnasDto> newdatosColumnasDtos = conectarSqLite.plantillaUsoDatos();
         newdatosColumnasDtos.get(0).setDatoColumna("Steve");
         
         int i = conectarSqLite.ActualizarDatos(newdatosColumnasDtos, 16);       
         
    Igualmente que en el punto 5) devuelve el id de la fila, pero si se presenta un error devolvera un valor negativo
    
    
       switch (aLong){
            case 0:{
                //no se pudo insertar
            }break;
            case -1:{
                //"Datos incompletos para ser guardados", faltan datos para insertar en la fila
            }break;
            case -2:{
                //error procesar datos, es posible que un dato se haya enviado en un formato incorrecto, por ejemplo, para insertar un                   //boolean envie un String y en la conversion el sistema detecto un error, por eso es importante conocer el id de columna
            }break;
        }
        
  
7) Leer la tabla:

  Para leer la tabla esta el comando:
  
        DatosTabla datos = conectarSqLite.LeerTabla();
        
 en este campo tenemos toda la tabla, para analizar estos datos solo es suficiente recorrer en dos for los datos, así:
 
        for (int indiceFilas = 0; indiceFilas < datos.getTablaCompleta().size(); indiceFilas++) {
            Fila fila = datos.getTablaCompleta().get(indiceFilas);
            Log.e("inicio fila", String.valueOf(indiceFilas));
            for (int indiceColumna = 0; indiceColumna < fila.getFila().size(); indiceColumna++) {
                DatosColumna columnas = fila.getFila().get(indiceColumna);
                Log.e(columnas.getNombreColumna(), columnas.getDatoColumna());
            }
        }
 
 
  


