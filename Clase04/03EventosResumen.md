### **Introducción a los Eventos en Solidity**

¡Hola! Hoy te voy a contar sobre algo super útil en el mundo de los contratos inteligentes: los eventos en Solidity. Piensa en los eventos como esos avisos que te llegan al móvil cuando pasa algo importante. En el caso de los contratos inteligentes, nos ayudan a saber qué está pasando por dentro sin necesidad de estar revisando todo el tiempo.

#### **¿Para qué sirven los eventos?**

Imagina que estás en una app donde puedes enviar y recibir ether (que es como la moneda del mundo Ethereum). Cada vez que envías o recibes, o incluso cuando algo importante cambia dentro del contrato, se genera un evento. Es como recibir una notificación que te dice: "Oye! Algo importante acaba de pasar."

Por ejemplo, si alguien actualiza el saldo de su cuenta, envía ether a alguien más, o cambia el dueño de algún activo digital, ahí es donde los eventos entran en juego.

#### **Usos Comunes de los Eventos:**
Cambios de Estado: Notificar actualizaciones en variables vitales del contrato, como saldos de cuentas o propiedad de activos digitales.
Transacciones de Activos: Seguir el movimiento de ethers o tokens hacia y desde el contrato.
Interacciones Externas: Informar sobre interacciones con sistemas externos, como oráculos u otros contratos inteligentes.

>Los eventos mejoran la transparencia y la trazabilidad en la ejecución de contratos y actúan como un puente de comunicación entre contratos inteligentes y el mundo externo.


### **Sintaxis Básica de los Eventos**

Los eventos se declaran utilizando la palabra clave **`event`** seguida de un nombre de evento y una lista de parámetros que describen los datos asociados. La sintaxis es sencilla:

a. Declaración de Eventos:

Para definir un evento, debes declararlo dentro del contrato. Una declaración de evento consta del nombre del evento, una lista de parámetros (si los hay) y sus tipos de datos. Aquí tienes un ejemplo:

```solidity
contract MiContrato {
  event NuevaTransaccion(uint indexed idTransaccion, address remitente, uint monto);

  // Resto del código del contrato...
}

```

En este ejemplo, definimos un evento llamado "NuevaTransaccion" que toma tres parámetros: idTransaccion (un número entero sin signo), remitente (una dirección Ethereum) y monto (un número entero sin signo).

b. Emisión de Eventos:

Para emitir un evento dentro del contrato, utilizas la palabra clave **`emit`** seguida del nombre del evento y cualquier parámetro necesario. Aquí tienes un ejemplo de emisión del evento NuevaTransaccion:

```solidity
function realizarTransaccion(address _receptor, uint _monto) public {
  // Lógica de la transacción...

  emit NuevaTransaccion(idTransaccion, msg.sender, _monto);

  // Resto del código de la función...
}

```

En este ejemplo, emitimos el evento NuevaTransaccion con los valores de idTransaccion, msg.sender (la dirección del llamador) y _monto.

### **Registro y Propagación de Eventos**

Los eventos juegan un papel vital en la divulgación de información fuera del contrato, permitiendo el registro y la comunicación eficientes de cambios significativos.

### **Características Clave de la Propagación de Eventos:**

- **Almacenamiento Económico:** Los eventos no almacenan datos directamente en la cadena de bloques, lo que reduce significativamente los costos de transacción.
- **Transmisión de Información:** Los eventos actúan como mensajeros, transmitiendo información relevante al mundo exterior, que puede ser consultada utilizando lenguajes como JavaScript.
- **Suscripciones en Tiempo Real:** Utilizando bibliotecas como web3.js, las interfaces de usuario o los servidores pueden suscribirse para recibir notificaciones sobre cambios en el contrato, facilitando interacciones dinámicas con el contrato.
- **Registro de Cambios Significativos:** Los eventos se utilizan para registrar actualizaciones cruciales dentro del contrato, como transacciones de activos o actualizaciones de estado.

#### **Algo más que debes saber**

Aunque los eventos son increíbles para notificar a las aplicaciones externas sobre lo que pasa en los contratos, tienen una limitación: otros contratos inteligentes no pueden escuchar estos eventos directamente. Además, siempre hay que tener cuidado con la seguridad y la privacidad, especialmente al decidir qué información incluimos en estos eventos para no revelar nada sensible.

