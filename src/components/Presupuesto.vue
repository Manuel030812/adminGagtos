<template>
    <form class="presupuesto"
        @submit.prevent="definirPresupuesto"
    >
        <Alerta
            v-if="error"
            > 
            {{ error }}
        </Alerta>
        <div class="campo">
            <label for="">Definir presupuesto</label>
            <input id="nuevoPresupuesto"
            class="nuevoPresupuesto" type="number" placeholder="Añade tu presupuesto " :type="Number" 
                min="0"
                v-model.number="presupuesto"
            
            />
        </div>
        <input type="submit"  class="submit" value="Definir presupuesto" />
    </form>
</template>

<script setup>
import { ref } from 'vue';
import Alerta from './Alerta.vue';

const presupuesto = ref(0);
const error = ref('');
const emit = defineEmits(['definir-presupuesto']);


const definirPresupuesto = () => {
    if (presupuesto.value <= 0 || presupuesto.value === '') {
        error.value = 'presupuesto no valido';

        setTimeout(() => {
        error.value = '';
        }, 3000);
        return;
    }

    emit('definir-presupuesto', presupuesto.value);
    
};





</script>

<style scoped>

.presupuesto {
    width: 100%;

}
.campo{
    display: grid;
    gap: 2rem;

}
.presupuesto label {
    font-size: 2.8rem;
    color: var(--azul);
    text-align: center;
}
.presupuesto input[type="number"] {
    background-color: var(--gris-claro);
    border-radius: 1rem;
    padding: 1rem;
    border: none;
    font-size: 2.2rem;
    text-align: center;

    
}

.presupuesto input[type="submit"] {
    background-color: var(--azul);
    border-radius: 1rem;
    padding: 1rem;
    border: none;
    font-size: 2.2rem;
    margin-top: 2rem;
    color: var(--blanco);
    font-weight: 900;
    width: 100%;
    text-align: center;
    transition: background-color 0.3s ease;
    
    
}
.presupuesto input[type="submit"]:hover{
    background-color: #1048a4;  
    cursor: pointer;
      
}
</style>