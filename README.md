# Projects
Actividades enfocadas en la formacion de Oracle y Alura LATAM

let amigos = [];

function adicionarAmigo() {
    const input = document.querySelector("input");
    const nombre = input.value.trim();
    
    if (nombre === "") {
        alert("Por favor, ingrese un nombre válido.");
        return;
    }
    
    if (amigos.includes(nombre)) {
        alert("Este nombre ya ha sido agregado.");
        return;
    }
    
    amigos.push(nombre);
    input.value = "";
    actualizarLista();
}

function actualizarLista() {
    const lista = document.querySelector("#lista-amigos");
    lista.innerHTML = "";
    amigos.forEach(amigo => {
        const li = document.createElement("li");
        li.textContent = amigo;
        lista.appendChild(li);
    });
}

function sortearAmigo() {
    if (amigos.length < 2) {
        alert("Debe haber al menos dos participantes para realizar el sorteo.");
        return;
    }
    
    let asignaciones = {};
    let disponibles = [...amigos];
    
    amigos.forEach(amigo => {
        let posibles = disponibles.filter(a => a !== amigo);
        if (posibles.length === 0) {
            sortearAmigo();
            return;
        }
        let elegido = posibles[Math.floor(Math.random() * posibles.length)];
        asignaciones[amigo] = elegido;
        disponibles = disponibles.filter(a => a !== elegido);
    });
    
    mostrarResultados(asignaciones);
}

function mostrarResultados(asignaciones) {
    const resultado = document.querySelector("#resultado");
    resultado.innerHTML = "";
    
    for (let amigo in asignaciones) {
        const p = document.createElement("p");
        p.textContent = `${amigo} -> ${asignaciones[amigo]}`;
        resultado.appendChild(p);
    }
}
