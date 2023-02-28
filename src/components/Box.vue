<template>
    <div class="box has-text-weight-bold" :style="estilos">
        <slot></slot>
    </div>
</template>

<script lang="ts">
import { defineComponent, DefineComponent } from 'vue';

export default defineComponent({
    name: 'BoxContainer',

    data () {
        return {
            estilos: {
                backgroundColor: '#FAF0CA'
            }
        }   
    }
})
</script>