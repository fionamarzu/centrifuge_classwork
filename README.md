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
