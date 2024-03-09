# lab01- sumador 

Nombre: Johan Hernan Lopez Alonso

## Descripcion de la practica
En este laboratorio se realizara el analisis, comprension y manipulacion de la descripcion en verilog de un sumador de 1bit con el objetivo de familizarse con el entorno de desarrollo Quartus y la herramienta de simulacion Questa. Se realizara la creacion de mi primer proyecto en quartus configurando la asignacion de dos diferentes Top-level entity, cada uno con descripciones del sumador distintas, se simularan y compararan ambas descripciones para llegar a unas conclusiones finales.

## informe de laoratorio

### 1) Sum1bcc_primitive:
En este codigo se crea un sumador de 1 bit siguiendo la logica combinacional previamente dada, en primer lugar se define el modulo sum1bcc_primitive con todas sus entradas y salidas, despues de definen los wires o cables necesarios para conectar las puertas logicas instanciadas en seguida, a cada puerta logica se le asigna una conexion de salida y sus entradas en ese orden. 

''' 

    modules sum1bcc_primitive (A, B, Ci,Cout,S); //creacion de bloque
      input  A; //sin especificar es igual a var de 1-bit
      input  B;
      input  Ci;
      output Cout;
      output S;
  
      wire a_ab; //definir cables
      wire x_ab;
      wire cout_t;
  
      and(a_ab,A,B); //Definir compuestas logicas
      xor(x_ab,A,B); //(conexion salida,entreda,entrada)
  
      xor(S,x_ab,Ci); //S=salida final
      and(cout_t,x_ab,Ci);
  
      or (Cout,cout_t,a_ab);
    end module
  
'''

### 2) Sum1bcc:
en este caso se crea el mismo sumados de 1bit (siguiendo la misma logica) pero con una descripcion distinta, vemos que el modulo se incia de la misma forma, sin embargo en lugar de describir cada compuerta y cable, se toma un enfoque mas directo definiendo un registro de 2 bits que almacenará el resultado de la suma [s,cout] , luego se declara un ciclo always que se ejecuta cada que detecta un cambio en las entradas y contiene la logica conbinacional. Es importante resaltar que st puede almacenar el reslutado de la suma ya que se definio con 2bits.

´´´

    module sum1bcc (A, B, Ci,Cout,S);

       input  A;
       input  B;
       input  Ci;
       output Cout;
       output S;
  
       reg [1:0] st; //registro de 2 bist
  
       assign S = st[0];
       assign Cout = st[1]; //se asignan las salidas al registro
  
       always @ ( * ) begin //ciclo que se ejecuta cuando las entradas cambian
          st  =   A+B+Ci; //Aqui esta la logica del sumador
       end
    
    endmodule

´´´
### ¿Como simular?
Para simular cada archivo (sum1bcc y sum1bcc_primitive) es necesario:
- a) Instalar la herramienta de simulacion elegida (Questa) y asignarla dentro de quartus especificando su ruta de ejecucion.
- b) Asignar la Top-level entity a el archivo que se desea simular.
- c) Sintetizar y analizar
Una vez realizado esto se corre la simulacion y Questa se despliega automaticamente; para realizar la simulacion del segundo archivo sin crear dos proyecto o tener otro quartus ejecutandose, se debe finalizar la primera simulacion y hacer los pasos b) y c).

### Resultados de simulacion:

#### sum1bcc_primitive


#### sum1bcc


### Conclusiones:
- Exinten varias formas validas de describir circuitos electronicos en Verilog-
- Las herramientas de simulacion permiten verificar el correcto funcionamiento de nuestros modelos.


