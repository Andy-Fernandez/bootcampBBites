Los metodos sirven para comuncar que algo a sucedido en el contrato inteligente, por ejemplo, si alguien envio ether a un contrato, si alguien retiro ether de un contrato, si alguien cambio un valor de un mapping, etc.

"alguea ha actualizado una varaibe"
"alguien ha enviado ether"
"alguien ha retirado ether"
"alguien ha cambiado un valor de un mapping"
-> Eventos

Y la forma en la que se comunican es a traves de eventos.

Entonces desde un contrato inteligente tu puedes porpagar información hacia un backend o hacia un frontend a traves de eventos. Sirve como un puente de comunicación entre el contrato inteligente y el mundo exterior.

Y tu deceides que información quieres propagar a traves de eventos, le idea es que sea un cambio significativo en el contrato inteligente.

### Propiedaes
ALMACENAMIENTO ECONÓMICO, una característica de los eventos es que no almacenan información en la blockchain, por lo que son económicos. Ya que usando eventos es mucho más económico que guardar información en una variable.
PROPAGAR INFORMACIÓN FUERA
SE HACEN QUERIES A LA DATA (JS) En el frontend o en el backend, se pueden hacer queries con JS a la data que se propaga a través de eventos.
SUBSCRIPCIÓN DEL FRONT Y/O EL BACK, para que puedan suscribirse a los eventos se puede hacer a través de web3.js, por ejemplo generando algo parecido a un socket.
REGISTRA CAMBIOS SIGNIFICATIVOS

Limitaciones:
- Otro contrato inteligente no puede escuchar eventos de otro contrato inteligente. En otras palabras no hay forma en la que el evento de un contrato disparte un método en otro contrato.