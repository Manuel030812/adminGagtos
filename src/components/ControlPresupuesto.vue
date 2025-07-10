<template>
    <div class="dosColumnas">
        <div class="contenerdorGrafico">
            <img :src="imagen" alt="">

        </div>

        <div class="contenedorPresupuesto">

            <button
                class="reset-app"
            >
            reseter presupuesto

            </button>
            <p>
                <samp>Presupuesto:</samp>
                ${{ presupuesto }}
            </p>
             <p>
                <samp>Dispolible:</samp>
                $   {{ disponible }}
            </p>
             <p>
                <samp>Gastado:</samp>
                $0
            </p>

        </div>

    </div>
</template>

<script setup>
import imagen from '../assets/img/grafico.jpg';

const props = defineProps({
    presupuesto: {
        type: Number,
        required: true
    },
    disponible: {
        type: Number,
        required: true
    }
});

</script>

<style scoped>

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