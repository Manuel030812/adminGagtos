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
                $0
            </p>
             <p>
                <samp>Dispolible:</samp>
                $0
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

</script>

<style scoped>

</style>