<script>
import CreateAndEdit from "../../../shared/components/create-and-edit.component.vue";

export default {
  name: "aging-create-and-edit",

  components: { CreateAndEdit },

  props: {
    item: null,
    visible: Boolean
  },

  data() {
    return {
      submitted: false,
      barrelTypes: [
        { label: "French Oak", value: "French Oak" },
        { label: "American Oak", value: "American Oak" },
        { label: "Hungarian Oak", value: "Hungarian Oak" },
        { label: "Stainless Steel", value: "Stainless Steel" },
        { label: "Clay Amphorae", value: "Clay Amphorae" }
      ],
      inspectionResults: [
        { label: "Passed", value: "Passed" },
        { label: "Failed", value: "Failed" },
        { label: "Needs Review", value: "Needs Review" },
        { label: "Re-inspection Required", value: "Re-inspection Required" }
      ]
    }
  },

  methods: {
    onCancelRequested() {
      this.$emit('cancel-requested-aging');
    },

    onSaveRequested() {
      this.submitted = true;
      this.$emit('save-requested-aging', this.item);
    }
  },

  created() {
    console.log('Aging Create and Edit Dialog component created');
  }
}
</script>

<template>
  <div>
    <create-and-edit :entity="item" :visible="visible" entity-name="Aging"
                     @canceled-shared="onCancelRequested"
                     @saved-shared="onSaveRequested">

      <template #content>

        <pv-float-label class="mt-5 w-full">
          <label for="batch_id">Batch ID</label>
          <pv-input-text id="batch_id" v-model="item.batchId"
                         :class="{ 'p-invalid': submitted && !item.batchId }"/>
        </pv-float-label>

        <div class="mt-5 w-full">
          <label for="barrel_type" class="block text-sm mb-1">Barrel type</label>
          <pv-dropdown id="barrel_type"
                       v-model="item.barrelType"
                       :options="barrelTypes"
                       option-label="label"
                       option-value="value"
                       placeholder="Select barrel type"
                       class="w-full"
                       :class="{ 'p-invalid': submitted && !item.barrelType }"/>
        </div>

        <pv-float-label class="mt-5 w-full">
          <label for="start_date">Start date</label>
          <pv-calendar id="start_date"
                       v-model="item.startDate"
                       date-format="yy-mm-dd"
                       class="w-full"
                       style="width: 100%;"
                       :class="{ 'p-invalid': submitted && !item.startDate }"/>
        </pv-float-label>

        <pv-float-label class="mt-5 w-full">
          <label for="end_date">End date</label>
          <pv-calendar id="end_date"
                       v-model="item.endDate"
                       date-format="yy-mm-dd"
                       class="w-full"
                       style="width: 100%;"
                       :class="{ 'p-invalid': submitted && !item.endDate }"/>
        </pv-float-label>

        <pv-float-label class="mt-5 w-full">
          <label for="aging_duration_months">Aging duration months</label>
          <pv-input-text id="aging_duration_months" v-model="item.agingDurationMonths"
                         :class="{ 'p-invalid': submitted && !item.agingDurationMonths }"/>
        </pv-float-label>

        <pv-float-label class="mt-5 w-full">
          <label for="inspections_performed">Inspections performed</label>
          <pv-input-text id="inspections_performed" v-model="item.inspectionsPerformed"
                         :class="{ 'p-invalid': submitted && !item.inspectionsPerformed }"/>
        </pv-float-label>

        <div class="mt-5 w-full">
          <label for="inspection_result" class="block text-sm mb-1">Inspection result</label>
          <pv-dropdown id="inspection_result"
                       v-model="item.inspectionResult"
                       :options="inspectionResults"
                       option-label="label"
                       option-value="value"
                       placeholder="Select result"
                       class="w-full"
                       :class="{ 'p-invalid': submitted && !item.inspectionResult }"/>
        </div>

      </template>

    </create-and-edit>
  </div>
</template>

<style scoped>
</style>
