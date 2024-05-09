La primera estrucurura que estudiaremos es pareciada a una tabla, es un hash table.

> El `mapping` es la estructura más usada en Solidity


Donde tenemos una clave y un valor asociado a esa clave, como se ve en la siguiente tabla de ejemplo:

En le codigo de Solidity creando el `mapping`:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.19;

contract MappingEdad {
    mapping(address => uint256) listaAddressAEdad;
}
```

| Dirección Ethereum (address) | Edad (uint256) |
|------------------------------|----------------|
| 0xAbC123...                  | 25             |
| 0xDeF456...                  | 30             |
| 0xGhI789...                  | 40             |


En esta tabla:

- La columna "Dirección Ethereum (address)" representa las direcciones de Ethereum que actúan como `claves` en el mapeo.
- La columna "Edad (uint256)" representa las edades, `valor`, asociadas a esas direcciones.

## Write -> Escirbiendo en un mapping
```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.19;

contract MappingEdad {
    mapping(address => uint256) listaAddressAEdad;

    function setAge(address _account, uint256 _edad) public {
        listaAddressAEdad[_account] = _edad;
    }
}
```

### Consideraciones
* Los mapeos no tienen un tamaño fijo, pueden crecer indefinidamente.
* Un mapping no es iterable, es decir, no podemos recorrerlo para obtener todos los elementos que contiene.

## Read -> Leyendo de un mapping

Si queresmos leer un valor de un mapping, simplemente accedemos a él con la clave correspondiente.

En el siguiente codigo, la función `getAge` recibe una dirección de Ethereum y devuelve la edad asociada a esa dirección.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.19;

contract MappingEdad {
    mapping(address => uint256) listaAddressAEdad;

    function getAge(address _account) public view returns (uint256) {
        return listaAddressAEdad[_account];
    }
}
```

Ejecutando la función `getAge` con la dirección `0xAbC123...` devolverá `25`.

## Delete -> Eliminando de un mapping

Al eliminar un elemento de un mapping, simplemente se asigna el valor `0` a la clave correspondiente.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.19;

contract MappingEdad {
    mapping(address => uint256) listaAddressAEdad;

    function deleteAge(address _account) public {
        delete listaAddressAEdad[_account];
    }
}
```

### Valores por defecto de un mapping
| Tipo de dato | Valor por defecto  |
|--------------|--------------------|
| uint256      | 0                  |
| int256       | 0                  |
| address      | 0x                 |
| bool         | false              |
| string       | "" (cadena vacía)  |
| bytes        | bytes32(0)         |
| mapping      | No tiene un valor por defecto específico |
| array        | [] (array vacío)   |
| struct       | Depende de los valores por defecto de sus miembros |
| enum         | El primer valor definido en la enumeración, que por defecto es 0 |


## Prpiedades del mapping

- **Un mapping tiene todos valores inicializados**: Un mapping en Solidity tiene todos sus valores inicializados con el valor predeterminado correspondiente a su tipo de dato. Por ejemplo, para un mapping de enteros (`mapping(uint256 => uint256)`), todos los valores serán inicializados en 0.

- **Tamaño máximo de 2^256**: El tamaño máximo de un mapping en Solidity es teóricamente 2^256. Esto se debe a que las claves de un mapping son de tipo `uint256`, que tiene un rango de valores de 0 a 2^256 - 1.

- **Un mapping no es iterable**: Un mapping en Solidity no es iterable como lo sería en JavaScript con `Object.keys()`. No hay una forma directa de recorrer todas las claves o valores de un mapping en Solidity.

- **De un mapping no se puede saber qué keys ya han sido utilizados**: No es posible determinar qué claves han sido utilizadas previamente en un mapping en Solidity. Tampoco se puede conocer la longitud de un mapping ni qué filas han sido actualizadas.

- **No puedo obetener la clave a partir del valor**: En Solidity, dado el valor de un mapping, no hay una forma directa de obtener la clave correspondiente. Los mappings están diseñados para acceder eficientemente a los valores a partir de las claves, pero no al revés.

- **Cada key del mapping viene a ser único e irrepetible**: Cada clave en un mapping de Solidity es única e irrepetible. No puede haber dos claves idénticas en un mismo mapping.

- **Clave como UUID**: En cierto sentido, una clave en un mapping puede ser vista como un UUID (Identificador Único Universal). Proporciona una forma única de identificar y acceder a los valores asociados en el mapping.

## Como contar los elementos de un mapping
Como los mappings no son iterables, no hay una forma directa de contar los elementos de un mapping en Solidity. Sin embargo, podemos mantener un contador separado para hacer un seguimiento del número de elementos en el mapping.

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.19;

contract MappingEdad {
    mapping(address => uint256) listaAddressAEdad;
    address[] public listaAddress;

    function setAge(address _account, uint256 _edad) public {
        listaAddressAEdad[_account] = _edad;
        listaAddress.push(_account);
    }
}
```

## Mapping de mappings
Para estructuras de datos más complejas, podemos tener mappings de mappings. Por ejemplo, un mapping que mapea una dirección a otro mapping que mapea una cadena a un entero.

| Address      | Historia | Lengua | Matematica | Geografia |
|--------------|----------|--------|------------|-----------|
| Juan (0x01)  | 20       | 20     | 20         | 20        |
| Maria (0x02) | 20       | 20     | 20         | 20        |
| Carlos (0x03)| 20       | 20     | 20         | 20        |
| Sara (0x04)  | 20       | 20     | 20         | 20        |


```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.24;

contract DoubleMapping {
    mapping(address => mapping(string => uint256)) notasPorAlumno;

    function setGradeForStudentAndCourse(
        address _wallet,
        string calldata _course,
        uint256 _grade
    ) public {
        notasPorAlumno[_wallet][_course] = _grade;
    }
}
```

## Tipos de datos

```solidity
// SPDX-License-Identifier: MIT
pragma solidity 0.8.19;

contract MappingDataTypes{
    mapping(bool => uint256) public boolToUint;
    mapping(string => address) public stringToAddress;
    mapping(uint256 => string) public uintToString;
    // y así con los demás tipos de datos
}
```
Lo unico que no se puede recibir como key en un mapping es un mapping, pero si se puede recibir como valor:

> `mapping(mapping => uint256)` no es valido, pero `mapping(uint256 => mapping)` si lo es.

| Types     | Key Type                  | Value Type               |
|-----------|---------------------------|--------------------------|
| boolean   | ✅                         | ✅                        |
| uint256   | ✅                         | ✅                        |
| int256    | ✅                         | ✅                        |
| address   | ✅                         | ✅                        |
| string    | ✅                         | ✅                        |
| enum      | ✅                         | ✅                        |
| bytes     | ✅                         | ✅                        |
| Contract  | ✅                         | ✅                        |
| mapping   | ❌                         | ✅                        |
| struct    | ❌                         | ✅                        |
| array type     | ❌                          | ✅                        |

Más artículos que podrían interesarte:
https://medium.com/p/22d800ece547/edit
https://medium.com/coinmonks/mapping-in-solidity-from-zero-to-hero-a5d7769fd03d