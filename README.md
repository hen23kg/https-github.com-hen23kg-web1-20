# https-github.com-hen23kg-web1-20
20 dom
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Listado de Nombres</title>
  <style>body {
    font-family: sans-serif;
    font-size: 13px;
  }
  
  .data-table {
    margin-top: 20px;
  }
  
  table,
  td,
  th {
    border-collapse: collapse;
    border: 1px solid #999;
    padding: 5px;
  }
  
  .msg-error {
    color: red;
    margin-bottom: 10px;
    font-size: 11px;
  }
  
  .form-group {
    margin-bottom: 10px;
  }
  
  .form-group input {
    border: 1px solid #999;
    padding: 5px;
  }
  
  .btn-save {
    border-width: 0px;
    background-color: #198754;
    color: white;
    padding: 5px 10px;
    border-radius: 3px;
    cursor: pointer;
  }
  
  .btn-delete {
    border-width: 0px;
    background-color: #dc3545;
    color: white;
    padding: 5px 10px;
    border-radius: 3px;
    cursor: pointer;
  }
  </style>

  <link rel="stylesheet" href="css/style.css">
</head>
<body onload="actualizarLista()">
  <h1>Formulario de Personas</h1>
  <hr>
  <div class="form-group">
    <label>Ingrese un nombre</label><br>
    <input type="text" id="input-nombre">
    <div class="msg-error" id="msg-error-nombre"></div>
  </div>
  <div class="form-group">
    <label>Ingrese la edad</label><br>
    <input type="number" id="input-edad" min="0">
    <div class="msg-error" id="msg-error-edad"></div>
  </div>
  <div class="form-group">
    <label>Ingrese el email</label><br>
    <input type="email" id="input-email">
    <div class="msg-error" id="msg-error-email"></div>
  </div>
  <input type="button" class="btn-save" value="Agregar persona" onclick="agregarPersona()">
  <h1>Listado de Personas</h1>
  <hr>
  <table class="data-table">
    <thead>
      <tr>
        <th>Eliminar</th>
        <th>Nombre</th>
        <th>Edad</th>
        <th>Email</th>
      </tr>
    </thead>
    <tbody id="lista-nombres">
      <tr>
        <td colspan="4">No hay personas registradas</td>
      </tr>
    </tbody>
  </table>
  <a href="https://github.com/hen23kg/web1-20.git">Repositorio en GitHub</a> // Inicializamos nuestro arreglo de personas con dos objetos
 const personas = [
  { nombre: "Juan Perez", edad: 18, email: "juan@ejemplo.com" },
  { nombre: "Maria Loza", edad: 21, email: "maria@ejemplo.com" }
];

function agregarPersona() {
  // Obtenemos el elemento para mostrar un error del nombre
  const msgErrorNombre = document.querySelector("#msg-error-nombre");
  // Borramos el contenido del elemento
  msgErrorNombre.innerHTML = "";

  // Obtenemos el elemento para mostrar un error de la edad
  const msgErrorEdad = document.querySelector("#msg-error-edad");
  // Borramos el contenido del elemento
  msgErrorEdad.innerHTML = "";

  // Obtenemos el elemento para mostrar un error del email
  const msgErrorEmail = document.querySelector("#msg-error-email");
  msgErrorEmail.innerHTML = "";

  // Obtenemos los inputs
  const inputNombre = document.querySelector("#input-nombre");
  const inputEdad = document.querySelector("#input-edad");
  const inputEmail = document.querySelector("#input-email");

  // Creamos una variable que indica si el formulario tiene error
  let hayError = false;

  // Obtenemos y validamos los valores de los inputs
  const nombre = inputNombre.value.trim();
  if (nombre === "") {
    msgErrorNombre.innerHTML = "Debe ingresar un nombre";
    hayError = true;
  }

  let edad = inputEdad.valueAsNumber;
  if (isNaN(edad)) {
    msgErrorEdad.innerHTML = "Debe ingresar una edad";
    hayError = true;
  } else if (!Number.isInteger(edad) || edad < 0) {
    msgErrorEdad.innerHTML = "Debe ingresar una edad válida";
    hayError = true;
  }

  const email = inputEmail.value.trim();
  if (email === "") {
    msgErrorEmail.innerHTML = "Debe ingresar un email";
    hayError = true;
  } else if (!esEmailValido(email)) {
    msgErrorEmail.innerHTML = "Debe ingresar un email válido";
    hayError = true;
  }

  // Si el formulario tiene algún error, salimos de la función
  if (hayError) {
    return;
  }

  // Si todos los valores son válidos, creamos una nueva persona
  const nuevaPersona = { nombre: nombre, edad: edad, email: email };

  // Ingresamos la nueva persona al arreglo
  personas.push(nuevaPersona);

  // Limpiamos los inputs
  inputNombre.value = "";
  inputEdad.value = "";
  inputEmail.value = "";

  // Actualizamos la lista de personas
  actualizarLista();
}

function esEmailValido(email) {
  const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return re.test(email);
}

function eliminar(i) {
  const respuesta = confirm("¿Está seguro que desea eliminar el nombre?");
  if (respuesta === false) {
    return;
  }
  personas.splice(i, 1);
  actualizarLista();
}

function actualizarLista() {
  const listaNombresHtml = document.getElementById("lista-nombres");
  if (personas.length === 0) {
    listaNombresHtml.innerHTML = `<tr><td colspan="4">No hay personas registradas</td></tr>`;
    return;
  }

  let html = "";
  for (let i in personas) {
    const persona = personas[i];
    html += `
      <tr>
        <td><input class="btn-delete" type="button" onclick="eliminar(${i})" value="Eliminar"></td>
        <td>${persona.nombre}</td>
        <td>${persona.edad}</td>
        <td>${persona.email}</td>
      </tr>
    `;
  }
  listaNombresHtml.innerHTML = html;
}

// Inicializamos la lista al cargar la página
actualizarLista();
  <script src="js/pr.js">
  </script>
</body>
</html>
