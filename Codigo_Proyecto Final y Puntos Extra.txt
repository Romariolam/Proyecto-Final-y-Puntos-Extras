var precio_base = 2000;

// Factores de recargo
var edad_18 = 0.1, edad_25 = 0.2, edad_50 = 0.3;
var casado_18 = 0.1, casado_25 = 0.2, casado_50 = 0.3;
var hijos_recargo = 0.2;
var propiedad_recargo = 0.35; // 35% por propiedad
var salario_recargo = 0.05;   // 5% del salario

while (true) {
    var recargo_total = 0;

    // Solicitar nombre
    var nombre = prompt("Ingrese su nombre o escriba 'SALIR' para finalizar:").toUpperCase();
    if (nombre === "SALIR") {
        alert("Gracias por usar nuestro sistema de cotización.");
        break;
    }

    // Validación de edad
    var edad;
    do {
        edad = parseInt(prompt("¿Cuántos años tiene? Ingrese solamente números"), 10);
        if (edad < 18 || isNaN(edad)) {
            alert("Edad inválida, por favor ingrese una edad correcta.");
        }
    } while (edad < 18 || isNaN(edad));

    var casado = prompt("¿Está casado actualmente? (Si/No)").toUpperCase();
    var edad_conyuge = 0;
    if (casado === "SI") {
        edad_conyuge = parseInt(prompt("¿Qué edad tiene su esposo/a?"), 10);
    }

    var hijos = prompt("¿Tiene hijos o hijas? (Si/No)").toUpperCase();
    var cantidad_hijos = 0;
    if (hijos === "SI") {
        cantidad_hijos = parseInt(prompt("¿Cuántos hijos tiene? Ingrese solo números"), 10);
    }

    // Nueva sección: Propiedades e ingresos
    var propiedades = parseInt(prompt("¿Cuántas propiedades posee? Ingrese solo números"), 10);
    if (isNaN(propiedades) || propiedades < 0) propiedades = 0;

    var salario = parseFloat(prompt("Ingrese su salario mensual en números (Ej: 1500.50)"), 10);
    if (isNaN(salario) || salario < 0) salario = 0;

    // Cálculo de recargos
    if (edad < 25) {
        recargo_total += precio_base * edad_18;
    } else if (edad < 50) {
        recargo_total += precio_base * edad_25;
    } else {
        recargo_total += precio_base * edad_50;
    }

    if (casado === "SI") {
        if (edad_conyuge < 25) {
            recargo_total += precio_base * casado_18;
        } else if (edad_conyuge < 50) {
            recargo_total += precio_base * casado_25;
        } else {
            recargo_total += precio_base * casado_50;
        }
    }

    recargo_total += cantidad_hijos * (precio_base * hijos_recargo);

    // Nuevos recargos
    recargo_total += propiedades * (precio_base * propiedad_recargo);
    recargo_total += salario * salario_recargo;

    // Precio final
    var precio_final = precio_base + recargo_total;

    // Resultado
    alert("Para el asegurado: " + nombre + 
          "\nRecargo total: $" + recargo_total.toFixed(2) + 
          "\nPrecio final: $" + precio_final.toFixed(2));
}