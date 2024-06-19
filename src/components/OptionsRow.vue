<template>
  <b-container class="container">
    <b-form @submit="onSubmit" class="options-container" inline>
      <label class="mr-sm-2 label-for-form" for="strike-price"
        >Strike Price:</label
      >
      <b-form-input
        name="strike-price"
        v-model="form.strike_price"
        class="mb-2 mr-sm-2 input form-elements"
        placeholder="0"
      ></b-form-input>

      <label class="mr-sm-2 label-for-form" for="type">Type:</label>
      <b-form-select
        v-model="form.type"
        class="mb-2 mr-sm-2 mb-sm-0 form-elements"
        :options="types"
        name="type"
        value="form.type"
      ></b-form-select>

      <label class="mr-sm-2 label-for-form" for="bid">Bid:</label>
      <b-form-input
        v-model="form.bid"
        name="bid"
        class="mb-2 mr-sm-2 input form-elements"
        placeholder="0"
      ></b-form-input>

      <label class="mr-sm-2 label-for-form" for="ask">Ask:</label>
      <b-form-input
        v-model="form.ask"
        name="ask"
        class="mb-2 mr-sm-2 input form-elements"
        placeholder="0"
      ></b-form-input>

      <label class="mr-sm-2 label-for-form" for="long-short"
        >Long or Short:</label
      >
      <b-form-select
        v-model="form.long_short"
        class="mb-2 mr-sm-2 mb-sm-0 form-elements"
        :options="longShorts"
        name="long-short"
        value="form.long_short"
      ></b-form-select>

      <label class="mr-sm-2 label-for-form" for="expiration-date"
        >Expiration Date:</label
      >
      <b-form-input
        v-model="form.expiration_date"
        id="expiration-date"
        name="expiration-date"
        class="mb-2 mr-sm-2 input form-elements"
        placeholder="0"
      ></b-form-input>

      <b-button
        type="submit"
        class="form-elements no-padding submit"
        variant="primary"
        >Plot</b-button
      >
      <b-button
        class="form-elements no-padding delete"
        @click="$emit('delete-row')"
        >delete</b-button
      >
    </b-form>
  </b-container>
</template>

<script setup>
import { defineEmits, ref, defineProps } from "vue";
const emit = defineEmits(["formData", "deleteId"]);
const props = defineProps({
  initialFormData: Object,
});

let form = ref(props.initialFormData);
const types = [{ text: "Choose...", value: form.type }, "Call", "Put"];
const longShorts = [
  { text: "Choose...", value: form.long_short },
  "long",
  "short",
];

function onSubmit(event) {
  event.preventDefault();
  emit("formData", form.value);
}
</script>

<style scoped>
.options-container {
  display: flex;
  align-items: baseline;
  justify-content: center;
  background: #344c64;
  border-radius: 8px;
  flex-wrap: wrap;
}
.container {
  width: 90%;
}

.form-elements {
  margin: 8px;
  height: 30px;
  border-radius: 8px;
}

.input {
  width: 70px;
}

.no-padding {
  padding: 0px !important;
}

#expiration-date {
  width: 15%;
  min-width: 100px;
}

.submit {
  background: #3572ef;
}

.submit:hover {
  background: #050c9c;
}

.delete {
  background: #e54f47;
}

.delete:hover {
  background: #a03630;
}

button {
  width: 50px;
  padding: 10px;
}

.label-for-form {
  color: white;
}
</style>
