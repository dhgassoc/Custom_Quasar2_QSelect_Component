<template>
  <q-page class="row items-center justify-evenly">
    <div class="q-gutter-lg">
      <q-card
        class="q-pa-xl bg-grey-1 shadow-1"
        style="height: 600px; width: 550px"
        ><q-card-section class="bg-yellow-3 text-black">
          <custom-qselect-component
            title="My Title"
            qsname="buildingselectid01"
            qslabel="Address"
            active
            :optionsArr="optionsArr"
            v-model="qsmodel"
          ></custom-qselect-component>
        </q-card-section>
      </q-card>
    </div>

    <div class="q-gutter-lg">
      <q-card
        class="q-pa-xl bg-grey-1 shadow-1"
        style="height: 300px; width: 450px"
        ><q-card-section class="bg-blue-3 text-white">
          <div class="text-h6">Q-Select Parent Component</div>
          <q-badge v-if="qsmodel" color="secondary" multi-line>
            qsmodel results: "{{ qsmodel }}"
          </q-badge>
        </q-card-section>
      </q-card>
    </div>
  </q-page>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import { QsmodelInterface } from 'components/models';
import CustomQselectComponent from 'components/CustomQselectComponent.vue';

export default defineComponent({
  name: 'IndexPage',
  components: { CustomQselectComponent },

  setup() {
    const optionsArr = ref<QsmodelInterface[]>([
      { id: 1, abbr: 'bld1', description: '1 Main St' },
      { id: 2, abbr: 'bld2', description: '2 Second St' },
      { id: 3, abbr: 'bld3', description: '3 Third St' },
      { id: 3, abbr: 'bld3', description: '4 Fourth St', inactive: true },
    ]);

    //const qsmodel = reactive<QsmodelInterface>(optionsArr.value[0]);
    const qsmodel = ref(null);

    return {
      qsmodel,
      optionsArr,
      qsname: ref(null),
      qslabel: ref(null),
    };
  },
});
</script>
