<script>
    import Boton from '$lib/Boton.svelte';
    import Formulario from '$lib/Formulario.svelte';
  
    let productos = [
      { id: 1, nombre: 'Harina', cantidad: 10, precio: 100 },
      { id: 2, nombre: 'Pasta', cantidad: 20, precio: 150 },
      { id: 3, nombre: 'Azucar', cantidad: 5, precio: 200 }
    ];
  
    let mostrarModal = false;
    let productoEditando = null;
    let busqueda = '';
  
    const productosFiltrados = () => {
      return productos.filter(
        (producto) =>
          producto.nombre.toLowerCase().includes(busqueda.toLowerCase())
      );
    };
  
    const agregarProducto = (producto) => {
      productos = [...productos, producto];
      mostrarModal = false;
    };
  
    const editarProducto = (producto) => {
      productos = productos.map((p) => (p.id === producto.id ? producto : p));
      mostrarModal = false;
    };
  
    const eliminarProducto = (id) => {
      if (confirm('¿Estás seguro de que quieres eliminar este producto?')) {
        productos = productos.filter((p) => p.id !== id);
      }
    };
  
    const abrirModal = (producto = null) => {
      productoEditando = producto;
      mostrarModal = true;
    };
  </script>
  
  <h1>Gestión de Productos</h1>
  
  <input
    type="text"
    bind:value={busqueda}
    placeholder="Buscar por nombre"
    class="input-busqueda"
  />
  
  <button class="boton-agregar" on:click={() => abrirModal()}>
    Agregar Producto
  </button>
  <center>
  <table>
    <thead>
      <tr>
        <th>Producto</th>
        <th>Cantidad</th>
        <th>Precio</th>
        <th>Acciones</th>
      </tr>
    </thead>
    <tbody>
      {#each productosFiltrados() as producto}
        <tr>
          <td>{producto.nombre}</td>
          <td>{producto.cantidad}</td>
          <td>{producto.precio}</td>
          <td>
            <Boton
              editarProducto={() => abrirModal(producto)}
              eliminarProducto={() => eliminarProducto(producto.id)}
            />
          </td>
        </tr>
      {/each}
    </tbody>
  </table>
</center>
  
  {#if mostrarModal}
    <Formulario
      {productoEditando}
      on:guardar={(e) => (productoEditando ? editarProducto(e.detail) : agregarProducto(e.detail))}
      on:cerrar={() => (mostrarModal = false)}
    />
  {/if}
  <style>
    body {
      background-color: #b1d4ec; 
      font-family: 'Arial', sans-serif;
      color: #333;
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh; 
      flex-direction: column; 
    }
  
    h1 {
      text-align: center;
      margin-bottom: 20px;
      font-size: 2rem;
      color: #000000;
    }
  
    .input-busqueda {
      display: block;
      width: 100%;
      max-width: 400px;
      margin: 20px auto;
      padding: 10px;
      border: 1px solid #bbdefb; 
      border-radius: 5px;
      font-size: 1rem;
      background-color: #ffffff;
      color: #333;
    }
  
    .input-busqueda:focus {
      outline: none;
      border-color: #90caf9;
      box-shadow: 0 0 5px rgba(144, 202, 249, 0.5);
    }
  
    .boton-agregar {
      margin: 20px auto;
      display: block;
      padding: 10px 20px;
      background-color: #64b5f6;
      color: rgb(10, 9, 9);
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1rem;
      transition: transform 0.5s ease;
    }
  
    .boton-agregar:hover {
      transform: rotate(360deg);
      background-color: #42a5f5;
    }
  
   
    .contenedor-tabla {
      display: flex;
      justify-content: center; 
      align-items: center;     
      width: 100%;             
      height: 100%;            
      box-sizing: border-box;
    }
  
    table {
      width: 100%;
      max-width: 800px;        
      border-collapse: collapse;
      background: #ffffff;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    }
  
    th, td {
      padding: 12px;
      text-align: left;
      border: 1px solid #bbdefb; 
    }
  
    th {
      background-color: #1d6097; 
      color: #ffffff;
    }
  
    tr:nth-child(even) {
      background-color: #e1f5fe; 
    }
  
    tr:nth-child(odd) {
      background-color: #bbdefb; 
    }
 
    button {
      padding: 6px 12px;
      border-radius: 5px;
      border: none;
      cursor: pointer;
      transition: background-color 0.3s ease, transform 0.2s ease;
    }
  
    button:first-child {
      background-color: #64b5f6; 
      color: white;
    }
  
    button:last-child {
      background-color: #42a5f5; 
      color: white;
    }
  
    button:hover {
      transform: scale(1.1); 
    }
  
    button:first-child:hover {
      background-color: #42a5f5;
    }
  
    button:last-child:hover {
      background-color: #1e88e5;
    }
  
    @media (max-width: 768px) {
      th, td {
        padding: 8px;
      }
  
      table {
        font-size: 14px;
      }
    }
  
    @media (max-width: 480px) {
      th, td {
        padding: 6px;
      }
  
      table {
        font-size: 12px;
      }
    }
  </style>
  