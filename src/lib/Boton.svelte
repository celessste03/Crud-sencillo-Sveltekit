<script>
    export let eliminarProducto;
    export let editarProducto;
  </script>
  
  <style>
    button {
      margin: 0 5px;
      padding: 5px 10px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      transition: transform 0.5s ease;
    }
  
    button:first-child {
      background-color: #3498db;
      color: white;
    }
  
    button:last-child {
      background-color: #dc3545;
      color: white;
    }
  
    button:hover {
      transform: rotate(360deg);
    }
  </style>
  
  <button on:click={editarProducto}>Editar</button>
  <button on:click={eliminarProducto}>Eliminar</button>
  
  