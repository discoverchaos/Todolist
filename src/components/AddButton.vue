<template lang="pug">
button.add-btn(@click="$emit('openModal')")
  img(src="../assets/img/edit.svg", alt="alt")
</template>
<script>
export default {};
</script>
<style lang="scss">
.add-btn {
  box-shadow: 0px 4px 8px 3px rgba(0, 0, 0, 0.15);
  filter: drop-shadow(0px 1px 3px rgba(0, 0, 0, 0.3));
  padding: 19px;
  background: linear-gradient(rgba(103, 80, 164, 0.11), rgba(103, 80, 164, 0.11)),#fffbfe;
  border-radius: 16px;
  position: fixed;
  right: 30px;
  bottom: 30px;
  cursor: pointer;
  border: none;
  outline: none;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>