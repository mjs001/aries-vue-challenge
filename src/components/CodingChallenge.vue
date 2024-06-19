<template>
  <div>
    <h1>Options Profit Calculator</h1>
    <h2>Options Contracts:</h2>
    <div
      v-for="(data, i) in formDataArr"
      :key="data.id"
      class="container-for-options"
    >
      <OptionsRow
        @formData="(data) => (form = data)"
        :initialFormData="data"
        @deleteId="(id) => (deleteId = id)"
        v-on:delete-row="deleteRow(i)"
      ></OptionsRow>
    </div>
    <b-button
      v-bind:class="formDataArr.length == 4 ? 'disabled' : 'addOptionsRowBtn'"
      @click="addOptionsContract"
      >Add Options Contract</b-button
    >
    <CustomGraph />
  </div>
</template>

<script setup>
import OptionsRow from "./OptionsRow.vue";
import CustomGraph from "./CustomGraph.vue";
import { ref, defineProps, watch } from "vue";
const props = defineProps({ optionsData: Array });
let formDataArr = ref(props.optionsData);

let form = ref(null);
let deleteId = ref(null);

function findMaxId() {
  let max = 0;
  if (formDataArr.value.length > 1) {
    formDataArr.value.forEach((row) => {
      const id = row.id;
      max = Math.max(max, id);
    });
  } else if (formDataArr.value.length == 1) {
    max = formDataArr.value[0].id;
  }
  max = max + 1;
  return max;
}

let newOptionsRow = ref({
  id: findMaxId(),
  strike_price: 0,
  type: "Call",
  bid: 0,
  ask: 0,
  long_short: "long",
  expiration_date: "2025-12-17T00:00:00Z",
});

function addOptionsContract() {
  newOptionsRow.value = {
    id: findMaxId(),
    strike_price: 0,
    type: "Call",
    bid: 0,
    ask: 0,
    long_short: "long",
    expiration_date: "2025-12-17T00:00:00Z",
  };
  if (formDataArr.value.length < 4) {
    formDataArr.value.push(newOptionsRow.value);
  }
}

function deleteRow(id) {
  formDataArr.value.splice(id, 1);
}

watch(form, (newFormRow) => {
  let index = formDataArr.value.findIndex((row) => row.id == newFormRow.id);
  formDataArr.value.splice(index, 1, newFormRow);
});
</script>

<style scoped>
.container-for-options {
  margin-bottom: 10px;
}

.addOptionsRowBtn {
  background: #3572ef;
}

.addOptionsRowBtn:hover {
  background: #050c9c;
}

.disabled {
  opacity: 0.6;
  cursor: not-allowed;
}
</style>
