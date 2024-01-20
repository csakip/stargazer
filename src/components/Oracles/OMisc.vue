<template>
  <div class="card-bg q-pa-xs">
    <o-input label="Story Complication" v-model="data.storyComplication" @roll="roll.storyComplication" />
    <o-input label="Story Clue" v-model="data.storyClue" @roll="roll.storyClue" />
    <o-input label="Anomaly Effect" v-model="data.anomalyEffect" @roll="roll.anomalyEffect" />
    <o-input label="Combat Action" v-model="data.combatAction" @roll="roll.combatAction" />
    <o-input label="Sector Trouble" v-model="data.sectorTrouble" @roll="roll.sectorTrouble" />
    <o-btns clear @clear="btns.Clear" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

import * as oracle from 'src/lib/oracles';

import OInput from './OInput.vue';
import OBtns from './OBtns.vue';

export default defineComponent({
  name: 'OMisc',
  components: { OInput, OBtns },
  setup() {
    const data = ref({
      anomalyEffect: '',
      combatAction: '',
      storyComplication: '',
      storyClue: '',
      sectorTrouble: '',
    });

    const roll = {
      storyComplication: () =>
        (data.value.storyComplication = oracle.roll('Starforged/Oracles/Misc/Story_Complication')),
      storyClue: () => (data.value.storyClue = oracle.roll('Starforged/Oracles/Misc/Story_Clue')),
      anomalyEffect: () => (data.value.anomalyEffect = oracle.roll('Starforged/Oracles/Misc/Anomaly_Effect')),
      combatAction: () => (data.value.combatAction = oracle.roll('Starforged/Oracles/Misc/Combat_Action')),
      sectorTrouble: () =>
        (data.value.sectorTrouble = oracle.roll('Starforged/Oracles/Character_Creation/Sector_Trouble')),
    };

    const btns = {
      Clear: () => {
        data.value = {
          anomalyEffect: '',
          combatAction: '',
          storyComplication: '',
          storyClue: '',
          sectorTrouble: '',
        };
      },
    };
    return {
      data,
      roll,
      btns,
    };
  },
});
</script>
