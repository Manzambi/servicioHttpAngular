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

    el formsModule lo usamos cuando queremos hacer un Biding direccional en dos sentidos escritura y lectura, el ejemplo es de la propiedad [(ngModule)]='nombredelatributo', por lo cual tenemoes que usar formsModule para usar esta propiedad.

    RoterModule.ForRoot es para declarar la constante o el atributo que posee las rutas, ej: RouterModule.forRoot(nombredelavariable), HttpClienteModule lo explicaremos a parte.


### providers

por aqui declaramos todos los servicios de nuestra app, todos los servicio

# Servicio Http

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
                        
                        
                              this.http.post('https://dbmiweb-38e47-default-rtdb.europe-west1.firebasedatabase.app/datos.json', nombredelavariable).subscribe( res=>console.log('se ha guardado', error=>console.log(error))
                            
                            }
  una vez hecho eso cuando usamos este metodo en nuestro servicio una vez ejecutado nos vamos a la pagina que se encuentra la base de datos y veremos un base de datos creado. 

  
                           obs: el tipo de base de datos que estamos a usar es la base de datos del tipo Realtime Database. pero hay un inconventiente usnado el metodo post en base de datos realtime porque duplica registro
                           toda vez que ejecutamos un post.

              

    
              
