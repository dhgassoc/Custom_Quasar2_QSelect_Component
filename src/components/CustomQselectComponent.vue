<template>
  <div class="q-pa-md" style="max-width: 300px">
    <div class="text-h6" v-if="title">{{ title }}</div>

    <div class="q-gutter-md">
      <q-select
        label-color="purple-8"
        color="purple-12"
        bg-color="purple-1"
        filled
        :name="qsname"
        :label="myLocals.QsLabelStr"
        option-value="id"
        option-label="description"
        option-disable="inactive"
        v-bind:options="optionsArr"
        v-model="theVModelRsp"
      />
    </div>

    <div class="debug q-mt-sm q-p-md q-gutter-sm shadow-3">
      <q-badge color="secondary" multi-line
        >DEBUG: CustomQselectComponent.vue</q-badge
      >
      <p>Items:</p>
      <ul>
        <li v-for="optionitem in optionsArr" :key="optionitem.id">
          {{ optionitem.id }} - {{ optionitem.description }} - aka
          {{ optionitem.abbr }}
        </li>
      </ul>
      <p>props.title: {{ title }}</p>
      <p>props.Active: {{ active ? 'yes' : 'no' }}</p>
      <p>props.qsname: {{ qsname }}</p>
      <p>props.qslabel: {{ qslabel }}</p>
      <p>QsLabelStr: {{ myLocals.QsLabelStr }}</p>
      <p>PrevQsLabelStr {{ myLocals.PrevQsLabelStr }}</p>

      <q-badge v-if="optionsArr" color="secondary" multi-line class="q-ma-sm">
        Model: "{{ optionsArr }}"
      </q-badge>
    </div>
  </div>
</template>

<script lang="ts">
import {
  PropType,
  computed,
  toRef,
  Ref,
  reactive,
  defineComponent,
  onMounted,
  onUpdated,
} from 'vue';
import { QsmodelInterface } from './models';

function useDisplayOption(optionsArr: Ref<QsmodelInterface[]>) {
  const optionCount = computed(() => optionsArr.value.length);
  return { optionCount };
}

export default defineComponent({
  name: 'CustomQselectComponent',

  props: {
    title: {
      type: String,
      required: true,
    },
    qsname: {
      type: String,
      required: true,
    },
    qslabel: {
      type: String,
      required: true,
    },
    optionsArr: {
      type: Array as PropType<QsmodelInterface[]>,
      default: () => [],
    },
    active: {
      type: Boolean,
    },
    modelValue: {
      type: Object as PropType<QsmodelInterface>,
      required: true,
      default: () => ({}), // Do not forget about default value
    },
  },

  emits: ['update:modelValue', 'qslabel'],

  setup(props, { emit }) {
    const myLocals = reactive({
      QsLabelStr: props.qslabel,
      PrevQsLabelStr: '',
    });

    const theVModelRsp = computed({
      get: () => props.modelValue,
      set: (newValue: QsmodelInterface) => {
        myLocals.QsLabelStr = props.qslabel + ':';
        emit('update:modelValue', newValue);
      },
    });

    onUpdated(() => {
      var tempStr = 'Select a ' + props.qslabel + '...';
      // only append once, to prevent infinate loop
      if (tempStr != myLocals.PrevQsLabelStr) {
        myLocals.PrevQsLabelStr = tempStr;
        myLocals.QsLabelStr = tempStr;
      }
    });

    onMounted(() => {
      myLocals.QsLabelStr = props.qslabel + '~onMounded():';
    });

    return {
      theVModelRsp,
      myLocals,
      ...useDisplayOption(toRef(props, 'optionsArr')),
    };
  },
});
</script>
