<template>
    <div class="modal">
        <div class="cerrarModal">
        <img :src="cerraraModal" alt="cerrar modal" 
            @click ="$emit('cerrar-modal')"
        />

        </div>

        <div class="contenedor contenedorFormulario"
            :class="[modal.animar ? 'animar': 'cerrar']"
           
        
        >

            <form class="nuevoGasto"
                @submit.prevent="agregarGasto"
                >
                <legend>
                    Añadir nuevo gasto
                </legend>

                <Alerta v-if="error">{{ error }}</Alerta>

                <div class="campo">
                    <label for="nombre">Nombre Gasto:</label>
                    <input type="text" id="nombre" placeholder="Añade el nombre del gasto"
                        :value="nombre"
                        @input="$emit('update:nombre', $event.target.value)"
                    />
                </div>
                <div class="campo">
                    <label for="cantidad">Cantidad Gasto</label>
                    <input type="number" id="cantidad" placeholder="Añade la cantidad del gasto ejem. 300"
                        :value="cantidad"
                        @input="$emit('update:cantidad', +$event.target.value)"
                    />
                </div>
                <div class="campo">
                    <label for="categoria">Categoria</label>
                    <select name="" id="categoria"
                        :value="categoria"
                        @input="$emit('update:categoria', $event.target.value)"
                    >
                        <option value="">--- Seleccione ---</option>
                        <option value="ahorro">Ahorro</option>
                        <option value="comida">Comida</option>
                        <option value="casa">Casa</option>
                        <option value="gastos">Gastos Varios</option>
                        <option value="ocio">Ocio</option>
                        <option value="salud">Salud</option>
                        <option value="suscripciones">Suscripciones</option>
                    </select>
                </div>
                <input 
                    type="submit" 
                    value="Añadir Gasto" 
                    class="boton" 
                
                
                />
            </form>

        </div>

    </div>
</template>

<script setup>
import {ref} from 'vue';
import cerraraModal from '../assets/img/cerrar.svg';
import Alerta from './Alerta.vue';

const error = ref('');

const emit = defineEmits(['cerrar-modal','guardar-gasto','update:nombre', 'update:cantidad', 'update:categoria']);
const props = defineProps({
  modal: {
    type: Object,
    required: true
  },
    nombre: {
        type: String,
        quired: true
    },
    cantidad: {
        type: [String,Number],
        required: true
    },
    categoria: {
        type: String,
        required: true
    }
});

const agregarGasto = () => {
  //validar que los campos no esten vacios
  const { nombre, cantidad, categoria } = props;
  if ([nombre, cantidad, categoria].includes('')) {
    error.value = 'Todos los campos son obligatorios';
    setTimeout(() => {
      error.value = '';
    }, 3000);
    return;
  }


  //validar que la cantidad sea un numero

    if (cantidad <= 0) {
        error.value = 'Cantidad no es válida';
        setTimeout(() => {
            error.value = '';
        }, 3000);
        return;
    }
    
    
    emit('guardar-gasto');
};

</script>

<style  scoped>


.modal{
    position: absolute;
    background-color: rgb(0 0 0 / 0.9);
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;

}

.cerrarModal{
    position: absolute;
    top: 3rem;
    right: 3rem;
}   
.cerrarModal img{
    width: 3rem;
    cursor: pointer;
}
.contenedorFormulario{
   transition-property: all;
   transition-duration: 300ms;
   transition-timing-function: ease-in;
   opacity: 0;
}
.contenedorFormulario.animar{
    opacity: 1;
}
.contenedorFormulario.cerrar{
    opacity: 0;

}
.nuevoGasto{
    margin: 10rem auto 0 auto;
    display: grid;
    gap: 2rem;
}
.nuevoGasto legend{
    font-size: 3rem;
    color: var(--blanco);
    text-align: center;
    font-weight: 700;
    
}
.campo{
   display: grid;
   gap: 2rem;

}
.nuevoGasto input,
.nuevoGasto select{
    background-color: var(--gris-claro);
    border-radius: 1rem;
    padding: 1rem;
    border: nano;
    font-size: 2.2rem;
}
.nuevoGasto label{
    color : var(--blanco);
    font-size: 3rem;
}
.nuevoGasto .boton{
    background-color: var(--azul);
    color: var(--blanco);
    font-weight: 700;
    cursor: pointer;
}
</style>