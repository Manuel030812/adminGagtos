<template>
    <div class="dosColumnas">
        <div class="contenerdorGrafico">

            <p class="porcentaje">{{ porcentaje }}%</p>
           <circle-progress
            :percent="porcentaje"
            :size="200"
            :border-width="15"
            :border-bg-width="15"
            fill-color="#3b82f6"
            emty-color="#f5f5f5"
           
           ></circle-progress>

        </div>

        <div class="contenedorPresupuesto">

            <button
                class="reset-app"
                type="button"
                @click="$emit('reset-app')"
            >
            reseter presupuesto

            </button>
            <p>
                <samp>Presupuesto:</samp>
                {{ formatearCantidad(presupuesto) }}
            </p>
             <p>
                <samp>Dispolible:</samp>
                   {{ formatearCantidad(disponible) }}
            </p>
             <p>
                <samp>Gastado:</samp>
                {{ formatearCantidad(gastado) }}
            </p>

        </div>

    </div>
</template>

<script setup>
import CircleProgress from 'vue3-circle-progress';
import 'vue3-circle-progress/dist/circle-progress.css';
import {formatearCantidad} from '../helpers';
import { computed } from 'vue';

defineEmits(['reset-app']);

const props = defineProps({
    presupuesto: {
        type: Number,
        required: true
    },
    disponible: {
        type: Number,
        required: true
    },
    gastado: {
        type: Number,
        required: true
    }
});


const porcentaje = computed(() => {
    return parseInt(((props.presupuesto - props.disponible)/props.presupuesto) * 100);
});

</script>

<style scoped>


.contenerdorGrafico {
    position: relative;

}
.porcentaje{
    position: absolute;
    margin: auto;
    top: calc(50% - 1.5rem);
    left: 0;
    right: 0;
    text-align: center;
    z-index: 100;
    font-size: 3rem;
    font-weight: 900;
    color: var(--gris-oscuro);

}

.dosColumnas {
    display: flex;
    flex-direction: column;
    
} 
.dosColumnas >:first-child{
    margin-bottom: 3rem;
}

@media (min-width: 768px) {
    .dosColumnas {
        flex-direction: row;
        gap: 4rem;
        align-items: center;
    }
    .dosColumnas >:first-child{
    margin-bottom: 0;
    }
}

.reset-app {
    background-color: #db2777;
    border: none;
    padding: 1rem;
    width: 100%;
    font-weight: 900;
    text-transform: uppercase;
    border-radius: 1rem;
    transition-property: background-color;
    transition-duration: 300ms;

}
.reset-app:hover {
    cursor: pointer;
    background-color: #f43f5e;
    color: var(--blanco);
}

.contenedorPresupuesto{
    width: 100%;


}
.contenedorPresupuesto p{
    font-size: 2.4rem;
    text-align: center;
    color: var(--gris-oscuro);


}
@media (min-width: 768px) {
    .contenedorPresupuesto p{
        font-size: 2.4rem;
        text-align: left;
    }
}

.contenedorPresupuesto samp {
    font-weight: 900;
    color: var(--azul);
}

</style>