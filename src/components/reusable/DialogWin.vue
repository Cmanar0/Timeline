<template>
  <div>
    <div @click="$emit('close')"></div>
    <dialog open>
      <header>
        <slot name="header">
          <h2>{{ title }}</h2>
        </slot>
      </header>
      <section>
        <slot name="default"> </slot>
      </section>
      <menu>
        <slot name="actions">
          <button @click="$emit('close')">Close</button>
        </slot>
      </menu>
    </dialog>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: false
    }
  },
  emits: ['close'] //we just mantion here that we do emit something from this component.
}
</script>

/* BaseDialogWindow.vue: */

<style scoped>
div {
  position: fixed;
  top: 0;
  left: 0;
  height: 110vh;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.75);
  z-index: 900;
}

dialog {
  position: fixed;
  top: 5vh;
  left: 10%;
  width: 80%;
  z-index: 1000;
  border-radius: 12px;
  border: none;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 0;
  margin: 0;
  overflow: hidden;
}

header {
  background-color: rgba(13, 81, 132, 255);
  color: white;
  width: 100%;
  padding: 1rem;
}

header h2 {
  margin: 0;
}

section {
  padding: 1rem;
}

menu {
  padding: 1rem;
  display: flex;
  justify-content: flex-end;
  margin: 0;
}

@media (min-width: 768px) {
  dialog {
    left: calc(50% - 20rem);
    width: 40rem;
  }
}
</style>
