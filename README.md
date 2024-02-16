# servicioHttpAngular
este es un repositorio donde se explica acerca del servicio http en angular

Para usar el servicio http lo primero que se hace es importar dicho servicio la importacion se hace desde el componente angular llamado app.module.ts
antes de seguir existe algunos criterios a saber a respecto de angular que que estan en @NgModule que tien la seguiente extructura:

@NgModule({

  declarations: [
  
   AppComponent,
  
  ],
  
  imports: [
  
  ],
  
  providers: [dataServices],
  
  bootstrap: [AppComponent]
  
})

### declarations
A continuacion explicamos en el apartado declaration declaramos todos los componentes que tenemos creados en nuestro proyecto angular, primero im portamos despues declaramos, por la cual se nosotros no lo declaramos no seran reconocidos en nuestro proyecto.

### imports
En el apartado imports importamos los modulos, todo lo que termina con  module como vimos en el apartado anterior una componente nosotros la generamos y tenemos que declrar pero un modulo no se declara por si ya existe dentro de paquete lo que se hace es importarlo desde el mismo proyecto en este aparato hacemos eso. algunos de los modelos que importamos y pusimos en el imports son:

          BroserModule, FormsModule, RouterModule.forRoot(), HttpClientModule etc.

    el formsModule lo usamos cuando queremos hacer un Biding direccional en dos sentidos escritura y lectura, el ejemplo es de la propiedad [(ngModel)]='nombredelatributo', 
    por lo cual tenemoes que usar formsModule para usar esta propiedad.

    OBS: la propiedad [(ngModel)] no funciona si los inputs estiveren dentro de un form..

    RoterModule.ForRoot es para declarar la constante o el atributo que posee las rutas, ej: RouterModule.forRoot(nombredelavariable), HttpClienteModule lo explicaremos a parte.


### providers

por aqui declaramos todos los servicios de nuestra app, todos los servicio

# Servicio Http
#### guardar los datos POST

como habiamos dicho dicho para poder usar el servivo http tenemos que importar desde nuestro imports httpClientModule, que se encuentra en la direccion 'angular/common/http'de la seguiente forma:

                import {HttpClientModule} from '@angular/common/http'
                
que es donde se encuentra nuestro servicio httpclientModule, a  continuacion lo metemos en import 

                imports: [
                            HttpClientModule
                         ],


creamos un servicio para poder hacer el uso de ella, y como creamos un servicio? usando ´ng g s nombredelservicio´ el servicio generado tendra dicha extructura:

                      import { Injectable } from '@angular/core';

                        @Injectable({
                        
                        
                          providedIn: 'root'
                        
                        })
                        
                        export class BorrarService {
                      
                          constructor() { }
                        }
o lo podemos crear manual en la capeta que querramos, y dando le el nombre data.service.ts o lo que querramos pero debemos asignar sempre la extesion .service.ts
Una vez creada el servicio dentro de nuestro contructor(en el servicio data) tenemos que inyectar dicho servicio, de la seguinete manera:

                        constructor(private nombredelavariable:HttpClient) { } 
                        
  pero para eso tenemos que importar primero HttpClient desde ´@angular/common/http´ es decir en nuestro fichero service.ts importamos HttpClient y en nuestro fichero module.ts importamos HttpClientModule es muy importante que sea asi la importacion en ambos lados eso es lo que hara que el servicio http sea reconocido en nuestro serviio. queda asi:


                          import {HttpClient} from '@angular/common/http'
                          export class BorrarService {
                      
                          constructor(private http: HttpClient) { }
                        }

el codigo de arriba solo de la forma que esta no es completa tenemos que add el yctable que es la propiedad que da el poder de las clases inyectar servicios solo basta adicionar antes de export class
  
                      

                       import {HttpClient} from '@angular/common/http'
                       import {Injectable}  from '@angular/core'
                        @Injectable()
                          export class BorrarService {
                      
                          constructor(private http: HttpClient) { }

                        }

  Una vez que se haya adicionado todo solo tenemos que hacer el uso del servicio, creamos un metodo y dentro del metodo usamos el servicio inyectado, por ejemplo si queremos guarar algo.

A continuacion mostraremos algunas propiedads del servicio Http que son 

                              get, put, post y delete
Si quqeremos crear un metodo de guaradr algo hacemos con el metodo post, ej:

                              guardarEmpleados(nombredelavariable:arry[]){
                                this.http.post('url')
                              }

lo que estamos recibiendo como parametro es un array que almacena datos, puede ser del cualquier tipo que quiera.
como estaremos trabajando con firebase la url que usaremos es la url donde se encuentra nusetra base de datos creado en firebase que la misma firebase nos proporciona: para eso es solo ir a la base de datos creada 
en firabase copiar la direccion y pegar nuestro codigo queda de la seguiente manera:

                          guardarEmpleados(nombredelavariable:arry[]){
                              this.http.post('https://dbmiweb-38e47-default-rtdb.europe-west1.firebasedatabase.app/datos.json', nombredelavariable)
                            }

  
    el codigo copiado es https://dbmiweb-38e47-default-rtdb.europe-west1.firebasedatabase.app/ pero es necesario que termina con datos.json por eso el codigo de arriba copiado lo adiccionamos datos.json
    en nuestor caso en metodo post recibe dos parametros ademas de la direccion debemos decirle que es que queremos almacenar, por eso le pasamos otro parametro que posee los datos que qeremos almacenar, pero nuestro codigo no esta al todo terminado para guardar en nuestra base de datos asi que tenemos que usar el obserservable para gestionar como respuestra del http. asi queda:

                        guardarEmpleados(nombredelavariable:arry[]){
                        
                        
                              this.http.post('https://dbmiweb-38e47-default-rtdb.europe-west1.firebasedatabase.app/datos.json', nombredelavariable).subscribe
                              ( res=>console.log('se ha guardado', error=>console.log(error))
                            
                            }
  una vez hecho eso cuando usamos este metodo en nuestro servicio una vez ejecutado nos vamos a la pagina que se encuentra la base de datos y veremos un base de datos creado. 

  
                           obs: el tipo de base de datos que estamos a usar es la base de datos del tipo Realtime Database. pero hay un inconventiente usnado el metodo post en base de datos 
                           realtime porque duplica registro toda vez que ejecutamos un post.


                          obs2: si quieres poder declarar sin la necesidad de inicializar va en tsconfig.json en la variable  "strict": false, este es el valor que tiene que tener 
              

#### obtener los datos GET

para obtener los datos usamos la propiedad get  asi queda:

                        this.http.get('https://dbmiweb-38e47-default-rtdb.europe-west1.firebasedatabase.app/datos.json')

  con este metodo estamos obteniendo la informacion que esta en la base de datos. generalmente el metodo devuelve un observable, para poder ver esta informacion hay que subscribirse:

                      this.http.get('https://dbmiweb-38e47-default-rtdb.europe-west1.firebasedatabase.app/datos.json').subscribe(res=>{console.log(res)})
                      
 El codigo de arriba obtiene los datos de nuestra base de datos y lo guarda en la varible temporal res, y se muestra a nuestra consola, ahora como hicimos para mostrar estos dadtos que estan almacenados en res 
 de modo que son observables.

 Para mostrar en la web tenemos que declarar una variable que coge los valores que se guardan en res. ej: this.variable = res
 si this.variable es un array y res es un observable dara error, lo que se puede hacer es ´this.variable = Object.values(res)´ quedando de la seguiente manera

                          this.http.get('https://dbmiweb-38e47-default-rtdb.europe-west1.firebasedatabase.app/datos.json').subscribe(res=>{this.variable = Object.values(res)})

De esta forma los valores se almacenan en la variable ´variable´ en nuestra componente y enseñarlo en la web.

### Actualizar datos PUT (update)

en Servicio data.service tenemos que crear un metodo que se encarga de actualizar los datos, para eso tendra que recebir dos parametros que son: el indice y el arreglo de valores que obtuvimos con el get.
el codigo de abajo ilustra la url que siempre usamos pero de esta vez concatenada con el indice de la variabla que posse estos valores. en este caso solo estariamos a coger un valor de entre tantos 

            actualizar(indice, variableModificada)
            {
                 url = 'https://dbmiweb-38e47-default-rtdb.europe-west1.firebasedatabase.app/datos/' + indice + '.json'
                     this.http.post(url, variableModificada).subscribe( res=>console.log('se ha actualizado o modificado', error=>console.log(error))
                              
            }

la ´variableModificada´ es la variable que lo modificamos en alguma otra clase o metodo, el nombre que ponemos alli es el nombre que declaremos en este caso apenas puse ´variableModificada´, esta varible
se pasa por parametro a nuestro servicio junto con el indice, el metodo put lo que hara en nuestra base de datos es buscar el indice dentro de la base de datos, una vez encontrada reemplazara los valores que 
se encuentran en este indice con el valor completo que estan en ´variableModificada´.
          
### Eliminar Datos (Delete)


en dataservice se usa el seguienete metodo:

    eliminar(indice)
                {
                     url = 'https://dbmiweb-38e47-default-rtdb.europe-west1.firebasedatabase.app/datos/' + indice + '.json'
                         this.http.delete(url).subscribe( res=>console.log('se ha eliminado', error=>console.log(error))
                                  
                }
este medodo eliminara los datos en la base de datos correspondiente al indice que le pasemos.
                        
### ng serve --proxy-config proxy.conf.json (comando usando en angular si queremos ejecutar una configuracion que hayamos hecho manual)
