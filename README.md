🗳️ Estación de Votación 🚀
¡Hola! Este es un contrato inteligente simple construido en Solidity que actúa como una cabina de votación digital. Es mi proyecto para demostrar el dominio de dos estructuras de datos fundamentales: Arreglos (Arrays) y Mapeos (Mappings) .

✨Conceptos Clave Aprendidos
Este proyecto me permitió dominar cómo manejar datos estructurados dentro de la Blockchain:

Estructura de Datos	Nombre en Código	¿Qué aprendí?
Arreglos (matrices)	uint[] public votes	✅ Almacenar listas de datos ( uint) y acceder a ellos por índice (ej: votes[3]). ¡Perfecto para contadores!
Mapeos (Mappings)	mapping(address => uint) public hasVoted	✅ Asociar una clave ( address) con un valor ( uint). ¡Es la base para prevenir el doble voto !
Lógica ( require)	require(hasVoted[msg.sender] == 0, ...)	✅ Implementar reglas de negocio. En este caso: 1 dirección = 1 voto , usando el valor por defecto 0de los mapeos.

Exportar a Hojas de cálculo
🛠️ Cómo Funciona la Magia
El contrato PollingStationes sorprendentemente simple pero poderoso:

Crea Candidatos (Constructor):

Al desplegar el contrato, le indicos cuántos candidatos existen (ej: 3).

Esto inicializa el Arreglo de Votos ( votes) con ceros: [0, 0, 0, 0]. (Usamos índice 1en adelante).

El Voto Inteligente ( votefunción):

Una dirección llama a la función vote(_candidateId).

Paso 1: Check-in 🧐: El contrato revisa el Mapeo ( hasVoted). Si el votante ya tiene un ID asociado (no es 0), ¡la transacción falla! (Evita el doble voto).

Paso 2: Contabilizar ➕: Incrementa el valor en el Arreglo de votos: votes[_candidateId]++.

Paso 3: Marcar 🔖: Graba el ID del candidato en el Mapeo para esa dirección: hasVoted[msg.sender] = _candidateId. ¡Ya no puedes votar más!

💻 El Código (Versión Limpia)
Aquí está el código central, sin comentarios, que funciona en Remix :

Solidez

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract PollingStation {
    uint[] public votes;
    mapping(address => uint) public hasVoted;

    constructor(uint _candidateCount) {
        votes = new uint[](_candidateCount + 1);
    }

    function vote(uint _candidateId) public {
        require(hasVoted[msg.sender] == 0, "You have already voted.");
        require(_candidateId > 0 && _candidateId < votes.length, "Invalid candidate ID.");

        votes[_candidateId]++;

        hasVoted[msg.sender] = _candidateId;
    }

    function getVoteCount(uint _candidateId) public view returns (uint) {
        require(_candidateId > 0 && _candidateId < votes.length, "Invalid candidate ID.");
        return votes[_candidateId];
    }
}
🎉 ¡Gracias!
Este ejercicio fue clave para entender cómo los arreglos manejan el almacenamiento secuencial y cómo los mapeos gestionan la identidad y las restricciones en Solidity.

¡A seguir construyendo la Web3! 🧱🌐