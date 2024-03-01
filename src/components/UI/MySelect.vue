<script>
export default {
  name: 'MySelect',
  props: {
    modelValue: {
      type: String,
    },
    options: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    changeOption(value) {
      this.$emit('update:modelValue', value);
    },
  },
};

</script>

<template>
  <select :value="modelValue" @change="changeOption($event.target.value)">
    <option disabled value="">pick something</option>
    <option 
      v-for="option in options" 
      :key="option.value" 
      :value="option.value"
    >
      {{ option.name }}
    </option>
  </select>
</template>

<style scoped></style>
