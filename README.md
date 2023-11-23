# centrifuge_classwork
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

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
        totalValueLocked += _value;

        emit AssetTokenized(msg.sender, _value);
    }

    function withdrawFunds() external onlyOwner {
        payable(owner).transfer(address(this).balance);
    }
}
Un contrato que utilice herencia podría estar diseñado para gestionar la tokenización y el manejo de RWA. Acá hay un ejemplo  para ilustrar cómo sería estructurar un contrato que herede de una base llamada CentrifugeBase


    contract Centrifuge is CentrifugeBase {

    event LoanFunded(address indexed borrower, uint amount);


    function fundLoan(address _borrower, uint _amount) external onlyOwner {

        emit LoanFunded(_borrower, _amount);
    }
}


Este es el contrato base, CentrifugeBase explicamos paso a paso lo que hace el codigo: 

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

LoanFunded: Es un evento específico de Centrifuge que se emite cuando se financia un préstamo.
Función Específica:

fundLoan(address _borrower, uint _amount): Una función específica de Centrifuge que permite al propietario financiar un préstamo. En este caso, simplemente emite el evento LoanFunded.
En resumen, Centrifuge hereda todas las características y funcionalidades de CentrifugeBase y puede añadir su propia lógica específica, como la financiación de préstamos. La herencia permite organizar y reutilizar código de manera efectiva.









