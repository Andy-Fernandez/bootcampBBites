# Estructura de un Contrato Inteligente en Solidity

Solidity no es solo un lenguaje de programación; también funciona como un framework. Esto significa que aprender su sintaxis no solo te permite escribir código, sino que también impacta directamente cómo interactuamos y modificamos la blockchain. En este documento, exploramos la estructura típica de un contrato inteligente en Solidity, destacando las mejores prácticas y limitaciones clave.

## Estructura de un Contrato Inteligente en Solidity


En Solidity, la organización del código dentro de un contrato es crucial para su claridad y mantenimiento. A continuación se presenta una estructura recomendada:


```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// Importaciones de otros contratos o bibliotecas
import "./OtherContract.sol";
import "./Library.sol";

// Declaración de eventos y errores
event LogEvent(address indexed user, uint amount);
error Unauthorized(address user);

// Interfaces y bibliotecas
// Una interfaz es un contrato parcial que define funciones externas y nos permite interactuar con otros contratos.
interface IAnotherContract {
    function someFunction() external view returns (bool);
}

// Una biblioteca es un contrato que contiene funciones que pueden ser reutilizadas en otros contratos que son methods abstaidos.
library SafeMath {
    function add(uint a, uint b) internal pure returns (uint) {
        uint c = a + b;
        require(c >= a, "SafeMath: addition overflow");
        return c;
    }
}

// Contrato principal
contract OrderLayoutContract {
    // Tipos de datos personalizados
    struct Data {
        uint id;
        address user;
    }
    enum State { Created, Locked, Inactive }

    // Variables de estado (state variables, que se almacenan en la blockchain o storage)
    // uint256, address, bool, string, bytes, etc.
    uint public constant VERSION = 1; // Constantes
    mapping(address => Data) private _userData; // Mappings

    // Modificadores
    modifier onlyOwner() {
        require(msg.sender == owner, "Not owner");
        _;
    }

    // Funciones del contrato
    constructor() {
        owner = msg.sender;
    }

    function setUser(address user, uint id) public onlyOwner {
        _userData[user] = Data(id, user);
        emit LogEvent(user, id);
    }

    // Funciones de fallback y receive
    fallback() external payable {
        // código customizado
    }
    
    receive() external payable {
        // código customizado
    }
}
```

### Las funciones tiene un orden por visibilidad y luego por tipo
- Constructor
- receive function
- fallback function
- external
- public
- internal
- 

```solidity
// Funciones del contrato
    constructor() {
        owner = msg.sender;
    }

    // Funciones de fallback y receive
    receive() external payable {
        // código customizado
    }

    fallback() external payable {
        // código customizado
    }

    function setUser(address user, uint id) public onlyOwner {
        _userData[user] = Data(id, user);
        emit LogEvent(user, id);
    }
```

### Consideraciones Importantes

- **Datos tipados:** Solidity es un lenguaje de programación fuertemente tipado, lo que significa que cada variable y función debe tener un tipo de datos explícito. Esto ayuda a prevenir errores y aclarar la intención del código.
- **Limitación de Tamaño:** El tamaño máximo del código de un contrato inteligente en Ethereum no debe exceder los 24 kilobytes. Esto es crítico porque los nodos de la red no aceptarán contratos que superen este tamaño.
- **Organización de Funciones:** Las funciones deben agruparse por visibilidad (`public`, `external`, `internal`, `private`) y luego por tipo (`view`, `pure`). Esto ayuda a otros desarrolladores a entender rápidamente las capacidades y restricciones del contrato.
- **Solamente podemon notar con un constructor, un receive function y un fallback function.**
