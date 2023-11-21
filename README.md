# centrifuge_classwork
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// Contrato base
contract CentrifugeBase {
    address public owner;
    uint public totalValueLocked;

    event AssetTokenized(address indexed asset, uint value);

    modifier onlyOwner() {
        require(msg.sender == owner, "Not the owner");
        _;
    }

    constructor() {
        owner = msg.sender;
    }

    function tokenizeAsset(uint _value) external onlyOwner {
        // Lógica para tokenizar un activo (simplificado)
        totalValueLocked += _value;

        emit AssetTokenized(msg.sender, _value);
    }

    function withdrawFunds() external onlyOwner {
        // Lógica para retirar fondos (simplificado)
        payable(owner).transfer(address(this).balance);
    }
}

// Contrato derivado que utiliza herencia
contract Centrifuge is CentrifugeBase {
    // Variables y funciones específicas de Centrifuge

    // Evento específico de Centrifuge
    event LoanFunded(address indexed borrower, uint amount);

    // Función específica de Centrifuge
    function fundLoan(address _borrower, uint _amount) external onlyOwner {
        // Lógica para financiar un préstamo (simplificado)
        emit LoanFunded(_borrower, _amount);
    }
}

Un contrato que utilice herencia podría estar diseñado para gestionar la tokenización y el manejo de activos del mundo real. Acá hay un ejemplo  para ilustrar cómo sería estructurar un contrato que herede de una base llamada CentrifugeBase
Este es el contrato base, CentrifugeBase. 

Variables de Estado:

owner: Es la dirección del propietario del contrato, establecido en el constructor.
totalValueLocked: Rastrea el valor total bloqueado en el contrato.
Evento:

AssetTokenized: Se emite cuando se tokeniza un activo. Al tokenizar un activo, el valor se suma a totalValueLocked.
Modificador:

onlyOwner: Un modificador que restringe ciertas funciones solo al propietario del contrato.
Constructor:

Establece al desplegar el contrato que el que lo desplegó es el propietario.
Funciones:

tokenizeAsset(uint _value): Permite al propietario tokenizar un activo y aumenta totalValueLocked.
withdrawFunds(): Permite al propietario retirar los fondos acumulados en el contrato.

Este es el contrato derivado, Centrifuge, que hereda de CentrifugeBase. 
Aquí está lo que hace:

Variables y Funciones Adicionales:

Puede tener sus propias variables y funciones específicas. En este caso, no hay ninguna en el código de ejemplo, pero podrían añadirse según las necesidades de Centrifuge.
Evento Específico:

LoanFunded: Es un evento específico de Centrifuge que se emite cuando se financia un préstamo.
Función Específica:

fundLoan(address _borrower, uint _amount): Una función específica de Centrifuge que permite al propietario financiar un préstamo. En este caso, simplemente emite el evento LoanFunded.
En resumen, Centrifuge hereda todas las características y funcionalidades de CentrifugeBase y puede añadir su propia lógica específica, como la financiación de préstamos. La herencia permite organizar y reutilizar código de manera efectiva.









