<p align="center">
  <a href="https://linkedin.com/in/wisrovi-rodriguez"><img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="https://wisrovi.dev"><img src="https://img.shields.io/badge/Author-wisrovi.dev-111827?style=for-the-badge&logo=google-chrome&logoColor=white" alt="Portal" /></a>
  <a href="https://orcid.org/0009-0005-0710-1861"><img src="https://img.shields.io/badge/ORCID-0009--0005--0710--1861-A6CE39?style=for-the-badge&logo=orcid&logoColor=white" alt="ORCID" /></a>
  <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge" alt="License" /></a>
</p>

# LibrarySqLite
libreria Android para usar las funciones de base de datos en el celular.

1) Crear el modelo de base de datos:

        TablaCrear tabla = new TablaCrear();
        tabla.setNombreTabla("WILI");
        List<ColumnaCrear> columnasDtos = new ArrayList<>();
        columnasDtos.add(new ColumnaCrear("nombre", TipoDatoSqLite.DatoString));
        columnasDtos.add(new ColumnaCrear("documento", TipoDatoSqLite.DatoEntero));
        columnasDtos.add(new ColumnaCrear("habilitado", TipoDatoSqLite.DatoBoolean));
        tabla.setColumnasDtos(columnasDtos);
        
2)  Conectar el modelo con una conexion estable de SqLite:

        ConectarSqLite conectarSqLite = new ConectarSqLite(getApplicationContext(), tabla);
        
3) Obtener una plantilla modificable para llenar nuevos datos, se usa esta plantilla para insertar nuevos datos o actualizar datos existentes

            List<DatosColumna> datosColumnas = conectarSqLite.plantillaUsoDatos();
            
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

---

## 👤 Autor & Afiliación Oficial

* **William Steve Rodriguez Villamizar (Wisrovi)**
* **Cargo:** Principal AI Engineer & Applied AI Solutions Architect | Scientific Researcher
* 📧 **Email:** [wisrovi.rodriguez@gmail.com](mailto:wisrovi.rodriguez@gmail.com)
* 🌐 **Portal Oficial:** [wisrovi.dev](https://wisrovi.dev)
* 💼 **LinkedIn:** [wisrovi-rodriguez](https://www.linkedin.com/in/wisrovi-rodriguez/)
* 🆔 **ORCID:** [0009-0005-0710-1861](https://orcid.org/0009-0005-0710-1861)
* 📦 **PyPI:** [pypi.org/user/wisrovi/](https://pypi.org/user/wisrovi/)
* 🐙 **GitHub:** [@wisrovi](https://github.com/wisrovi)
