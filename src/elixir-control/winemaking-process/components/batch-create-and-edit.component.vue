<script>
import CreateAndEdit from "../../../shared/components/create-and-edit.component.vue";

export default {
  name: "batches-create-and-edit",

  components: { CreateAndEdit },

  props: {
    itemBatch: null,
    visible: Boolean
  },

  data() {
    return {
      submitted: false,
      grapeVarieties: [
        { label: "Quebranta", value: "Quebranta" },
        { label: "Negra Criolla", value: "Negra Criolla" },
        { label: "Italia", value: "Italia" },
        { label: "Torontel", value: "Torontel" },
        { label: "Mollar", value: "Mollar" },
        { label: "Albilla", value: "Albilla" }
      ],
      vineyardOrigins: [
        { label: "Pisco", value: "Pisco" },
        { label: "Ica", value: "Ica" },
        { label: "Chincha", value: "Chincha" },
        { label: "Nazca", value: "Nazca" },
        { label: "Palpa", value: "Palpa" }
      ]
    }
  },

  methods: {
    onCancelRequested() {
      this.$emit('cancel-requested-batches');
    },

    onSaveRequested() {
      this.submitted = true;
      this.$emit('save-requested-batches', this.itemBatch);
    }
  },

  created() {
    console.log('Batches Create and Edit Dialog component created');
  }
}
</script>

<template>
  <create-and-edit :entity="itemBatch" :visible="visible" entity-name="Batch"
                   @canceled-shared="onCancelRequested" @saved-shared="onSaveRequested">

    <template #content>

      <pv-float-label class="mt-5">
        <label for="vineyard_code">Vineyard code</label>
        <pv-input-text id="vineyard_code" v-model="itemBatch.vineyardCode"
                       :class="{ 'p-invalid': submitted && !itemBatch.vineyardCode }" />
      </pv-float-label>

      <div class="mt-5">
        <label for="grape_variety" class="block text-sm mb-1">Grape variety</label>
        <pv-dropdown id="grape_variety"
                     v-model="itemBatch.grapeVariety"
                     :options="grapeVarieties"
                     option-label="label"
                     option-value="value"
                     placeholder="Select grape variety"
                     class="w-full"
                     :class="{ 'p-invalid': submitted && !itemBatch.grapeVariety }" />
      </div>

      <div class="mt-5">
        <label for="harvest_date" class="block text-sm mb-1">Harvest date</label>
        <pv-calendar id="harvest_date"
                     v-model="itemBatch.harvestDate"
                     date-format="yy-mm-dd"
                     class="w-full"
                     :class="{ 'p-invalid': submitted && !itemBatch.harvestDate }" />
      </div>

      <pv-float-label class="mt-5">
        <label for="grape_quantity">Grape quantity</label>
        <pv-input-text id="grape_quantity" v-model="itemBatch.grapeQuantity"
                       :class="{ 'p-invalid': submitted && !itemBatch.grapeQuantity }" />
      </pv-float-label>

      <div class="mt-5">
        <label for="vineyard_origin" class="block text-sm mb-1">Vineyard origin</label>
        <pv-dropdown id="vineyard_origin"
                     v-model="itemBatch.vineyardOrigin"
                     :options="vineyardOrigins"
                     option-label="label"
                     option-value="value"
                     placeholder="Select vineyard origin"
                     class="w-full"
                     :class="{ 'p-invalid': submitted && !itemBatch.vineyardOrigin }" />
      </div>

      <div class="mt-5">
        <label for="process_start_date" class="block text-sm mb-1">Start date</label>
        <pv-calendar id="process_start_date"
                     v-model="itemBatch.processStartDate"
                     date-format="yy-mm-dd"
                     class="w-full"
                     :class="{ 'p-invalid': submitted && !itemBatch.processStartDate }" />
      </div>

    </template>

  </create-and-edit>
</template>

<style scoped>
</style>
