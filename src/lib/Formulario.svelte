<script>
    import { createEventDispatcher, onMount } from 'svelte';
  
    export let productoEditando = null;
    
    let nombre = '';
    let cantidad = 0;
    let precio = 0;
  
    const dispatch = createEventDispatcher();
  
    onMount(() => {
      if (productoEditando) {
        nombre = productoEditando.nombre;
        cantidad = productoEditando.cantidad;
        precio = productoEditando.precio;
      }
    });
  
    const guardar = () => {
      if (!nombre.trim()) {
        alert("El nombre no puede estar vacío.");
        return;
      }
      if (cantidad <= 0) {
        alert("La cantidad debe ser mayor que 0.");
        return;
      }
      if (precio <= 0) {
        alert("El precio debe ser mayor que 0.");
        return;
      }
  
      const producto = { 
        id: productoEditando?.id || Date.now(), 
        nombre, 
        cantidad, 
        precio 
      };
  
      dispatch('guardar', producto);
    };
  </script>
  
  <div class="modal">
    <h2>{productoEditando ? 'Editar Producto' : 'Agregar Producto'}</h2>
    <input type="text" bind:value={nombre} placeholder="Nombre del Producto" />
    <input type="number" bind:value={cantidad} placeholder="Cantidad" />
    <input type="number" bind:value={precio} placeholder="Precio" />
  
    <div class="botones">
      <button class="guardar" on:click={guardar}>Guardar</button>
      <button class="cerrar" on:click={() => dispatch('cerrar')}>Cerrar</button>
    </div>
  </div>
  
  <style>
    .modal {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      background: #ffffff;
      padding: 25px;
      border-radius: 12px;
      box-shadow: 0 6px 30px rgba(0, 0, 0, 0.826);
      width: 90%;
      max-width: 400px;
      border: 1px solid #e0e0e0;
    }
  
    .modal h2 {
      margin: 0 0 20px 0;
      font-size: 1.5rem;
      color: #333333;
      text-align: center;
    }
  
    .modal input {
      display: block;
      width: 100%;
      margin: 10px 0;
      padding: 10px;
      border: 1px solid #cccccc;
      border-radius: 6px;
      font-size: 1rem;
      color: #333333;
      background-color: #f9f9f9;
      transition: border-color 0.3s ease, box-shadow 0.3s ease;
    }
  
    .modal input:focus {
      border-color: #3498db;
      box-shadow: 0 0 5px rgba(52, 152, 219, 0.5);
      outline: none;
    }
  
    .modal .botones {
      display: flex;
      justify-content: space-between;
      margin-top: 20px;
    }
  
    .modal button {
      padding: 10px 20px;
      border: none;
      border-radius: 6px;
      font-size: 1rem;
      cursor: pointer;
      transition: background-color 0.3s ease, transform 0.2s ease;
    }
  
    .modal button.guardar {
      background-color: #3498db;
      color: white;
    }
  
    .modal button.guardar:hover {
      background-color: #2980b9;
      transform: translateY(-2px);
    }
  
    .modal button.cerrar {
      background-color: #e74c3c;
      color: white;
    }
  
    .modal button.cerrar:hover {
      background-color: #c0392b;
      transform: translateY(-2px);
    }
  </style>
  