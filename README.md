import React, { useState } from "react";

const App = () => {
  const [formData, setFormData] = useState({
    nombre: "",
    apellidoPaterno: "",
    apellidoMaterno: "",
    fechaNacimiento: "",
  });

  const [rfc, setRFC] = useState("");

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData({ ...formData, [name]: value });
  };

  const generarRFC = () => {
    const { nombre, apellidoPaterno, apellidoMaterno, fechaNacimiento } = formData;

    if (!nombre || !apellidoPaterno || !fechaNacimiento) {
      alert("Por favor, llena todos los campos obligatorios.");
      return;
    }

    // Obtener las primeras letras del RFC
    const rfc =
      apellidoPaterno.slice(0, 2).toUpperCase() +
      (apellidoMaterno[0] || "").toUpperCase() +
      nombre[0].toUpperCase();

    // Formatear la fecha de nacimiento
    const [year, month, day] = fechaNacimiento.split("-");
    const fecha = year.slice(2) + month + day;

    // Homoclave ficticia
    const homoclave = "XX1";

    // RFC completo
    setRFC(rfc + fecha + homoclave);
  };

  return (
    <div style={{ padding: "20px", fontFamily: "Arial, sans-serif" }}>
      <h1>Generador de RFC</h1>
      <form
        onSubmit={(e) => {
          e.preventDefault();
          generarRFC();
        }}
      >
        <div>
          <label>
            Nombre:
            <input
              type="text"
              name="nombre"
              value={formData.nombre}
              onChange={handleChange}
              required
            />
          </label>
        </div>
        <div>
          <label>
            Apellido Paterno:
            <input
              type="text"
              name="apellidoPaterno"
              value={formData.apellidoPaterno}
              onChange={handleChange}
              required
            />
          </label>
        </div>
        <div>
          <label>
            Apellido Materno:
            <input
              type="text"
              name="apellidoMaterno"
              value={formData.apellidoMaterno}
              onChange={handleChange}
            />
          </label>
        </div>
        <div>
          <label>
            Fecha de Nacimiento:
            <input
              type="date"
              name="fechaNacimiento"
              value={formData.fechaNacimiento}
              onChange={handleChange}
              required
            />
          </label>
        </div>
        <button type="submit">Generar RFC</button>
      </form>
      {rfc && (
        <div>
          <h2>RFC Generado:</h2>
          <p>{rfc}</p>
        </div>
      )}
    </div>
  );
};

export default App;
