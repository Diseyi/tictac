<template>
    <div class="tic-tac-toe">
        <composition-tictac></composition-tictac>
        <!-- <option-tictac></option-tictac> -->
    </div>
</template>
  
<script lang="ts">
import { defineComponent } from 'vue';
import CompositionTictac from './components/compositionTictac.vue';
import OptionTictac from './components/optionTictac.vue';


export default defineComponent({
    components: {
        CompositionTictac,
        OptionTictac,
    },
});
</script>
  