Wordloads
Se encarga de realizar los procesos. Los **pods** son workloads realmente que funcionan teniendo dentro los contenedores y ofreciendonos los contenedores al entorno.
Los **pods** carecen de ciertas caracteristicas (replicas, escalamiento, update, rollback) que otros obejtos las tienen.

Estos otros objetos son los **deployments**. Los **deployments** van a ser los que envuelvan a los **pods**, de hecho todos los **controlers**, todos los **workloads** de este tipo van a envolver a los **pods** y que le dan una serie de caracteristicas:
- updates
- rollback
- comprobar y matener que funciona correctamente

Luego tenemos otros **workloads** como los **replica set**, son los encargados de hacer el escalado de los **pods** cuando es necesario, subir o bajar los **pods** de acuerdo a lo que el cluster tenga indicado.

Otro **wordloads** que son los **stateful set**, es un objeto que gestiona el despliegue y el escalado. Garantiza el orden y la unicidad de esos **pods**.

Luego tenemos los **daemon set**, es un componente que asegura todos los nodos del cluster van a tener una copia de un **pod**. 
Por ejemplo si anado un nuevo **worker node** dentro del cluster este componente va intentar a toda costa que haya un **pod** dentro del mismo.

Tambien tenemos los denominados **job**, es un componente que va crear uno o varios **pods** y se van asegurar de que un determinado numero de ellos se terminen satisfactoriamente

Tenemos otro el **cron job**, se hace de forma planificada con scheduler.

Estos componentes a su ves tienen asociado **controllers**, que su trabajo es continuamente controlando que el cluster esta correcto y los **pods** y los **workloads** que estan definidos se adaptan a lo que se definio.
Los **controllers** son de tipo loop que van consultando de ves en cuando el cluster y cada uno de sus componentes y van a intentar tenerlo en un estdo correcto.
