<template>
  <button :class="mode">
    <slot></slot>
    <!-- <base-button mode="flat"></base-button> -->
  </button>
</template>


<script>
export default {
  props: ['mode'],
};
</script>

<style scoped>
button {
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  background-color: #3a0061;
  border: 1px solid #3a0061;
  color: white;
  cursor: pointer;
}

button:hover,
button:active {
  background-color: #00b8c0;
  border-color: #270041;
}

.flat {
  background-color: transparent;
  color: #0074e4;
  border: none;
}

.flat:hover,
.flat:active {
  background-color: #a0edf1;

}
</style>