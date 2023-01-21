<template>
  <v-card v-if="selectedCat != null">
    <v-card-title>{{ selectedCat.name }}</v-card-title>
    <v-card-subtitle>{{ selectedCat.id }}</v-card-subtitle>
    <v-alert density="comfortable" type="success" variant="tonal">
      Unmodified
    </v-alert>
    <v-tabs v-model="cat_tab" color="blue" align-tabs="left">
      <v-tab :value="1">Properties</v-tab>
      <v-tab :value="2">Prizes (0)</v-tab>
    </v-tabs>
    <!-- Show a form of active (checkmark), Name (text), Count(Number) cant go past 99 Weighting (number), Background (number) -->
    <v-form v-if="cat_tab == 1">
      <v-container fluid>
        <v-switch
          label="Active"
          color="blue"
          type="checkbox"
          :true-value="1"
          :false-value="0"
          :model-value="selectedCat.active"
        />
        <v-text-field
          clearable
          label="Name"
          type="text"
          hide-details="auto"
          :model-value="selectedCat.name"
        />
        <v-text-field
          label="Count"
          type="number"
          :model-value="selectedCat.count"
          :counter="2"
          :rules="[
            (v) => v.length <= 2 || 'Count must be less than 2 characters',
          ]"
        />
        <v-text-field
          label="Weighting"
          type="number"
          :model-value="selectedCat.weighting"
        />
        <!-- TODO convert this into a dropdown -->
        <v-text-field
          label="Background"
          type="number"
          :model-value="selectedCat.background"
        />
      </v-container>
    </v-form>
  </v-card>
  <br />
  <v-alert
    v-if="selectedCat == null"
    color="red"
    type="error"
    dense
    variant="tonal"
    ><i>Nothing selected.</i></v-alert
  >
</template>

<script>
export default {
  name: 'Details',
  props: {
    selectedCat: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      cat_tab: null,
      active:
        this.selectedCat == null
          ? null
          : this.selectedCat.active == 1
          ? true
          : false,
    };
  },
  created() {
    console.log(this.selectedCat);
  },
};
</script>
