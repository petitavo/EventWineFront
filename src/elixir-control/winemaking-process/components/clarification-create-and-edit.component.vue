<script>
import CreateAndEdit from "../../../shared/components/create-and-edit.component.vue";

export default {
  name: "clarification-create-and-edit",
  components: { CreateAndEdit },

  props: {
    item: null,
    visible: Boolean
  },

  data() {
    return {
      submitted: false,
      clarificationMethods: [
        { label: "Bentonite", value: "Bentonite" },
        { label: "Cold Stabilization", value: "Cold Stabilization" },
        { label: "Centrifugation", value: "Centrifugation" },
        { label: "Gelatin", value: "Gelatin" },
        { label: "Kieselsol", value: "Kieselsol" },
        { label: "Egg white", value: "Egg white" }
      ]
    };
  },

  methods: {
    onCancelRequested() {
      this.$emit('cancel-requested-clarification');
    },

    onSaveRequested() {
      this.submitted = true;
      this.$emit('save-requested-clarification', this.item);
    }
  },

  created() {
    console.log('Clarification Create and Edit Dialog component created');
  }
};
</script>

<template>
  <div class="p-fluid">
    <create-and-edit :entity="item" :visible="visible" entity-name="Clarification"
                     @canceled-shared="onCancelRequested" @saved-shared="onSaveRequested">

      <template #content>

        <pv-float-label class="mt-5">
          <label for="batch_id">Batch ID</label>
          <pv-input-text id="batch_id" v-model="item.batchId"
                         :class="{ 'p-invalid': submitted && !item.batchId }" />
        </pv-float-label>

        <pv-float-label class="mt-5">
          <label for="products_used">Products used</label>
          <pv-input-text id="products_used" v-model="item.productsUsed"
                         :class="{ 'p-invalid': submitted && !item.productsUsed }" />
        </pv-float-label>

        <div class="mt-5">
          <label for="clarification_method" class="block text-sm mb-1">Clarification method</label>
          <pv-dropdown id="clarification_method"
                       v-model="item.clarificationMethod"
                       :options="clarificationMethods"
                       option-label="label"
                       option-value="value"
                       placeholder="Select clarification method"
                       class="w-full"
                       :class="{ 'p-invalid': submitted && !item.clarificationMethod }" />
        </div>

        <div class="mt-5">
          <label for="filtration_date" class="block text-sm mb-1">Filtration date</label>
          <pv-calendar id="filtration_date"
                       v-model="item.filtrationDate"
                       date-format="yy-mm-dd"
                       class="w-full"
                       :class="{ 'p-invalid': submitted && !item.filtrationDate }" />
        </div>

        <pv-float-label class="mt-5">
          <label for="clarity_level">Clarity level</label>
          <pv-input-text id="clarity_level" v-model="item.clarityLevel"
                         :class="{ 'p-invalid': submitted && !item.clarityLevel }" />
        </pv-float-label>

        <div class="mt-5">
          <label for="start_date" class="block text-sm mb-1">Start date</label>
          <pv-calendar id="start_date"
                       v-model="item.startDate"
                       date-format="yy-mm-dd"
                       class="w-full"
                       :class="{ 'p-invalid': submitted && !item.startDate }" />
        </div>

        <div class="mt-5">
          <label for="end_date" class="block text-sm mb-1">End date</label>
          <pv-calendar id="end_date"
                       v-model="item.endDate"
                       date-format="yy-mm-dd"
                       class="w-full"
                       :class="{ 'p-invalid': submitted && !item.endDate }" />
        </div>

      </template>

    </create-and-edit>
  </div>
</template>

<style scoped>
</style>
