<template>
  <div
    class="flex flex-row justify-start items-center"
  >
    <figure class="mr-6">
      <slot name="icon" />
    </figure>
    <section>
      <label
        class="block text-sm opacity-75"
        v-text="label"
      />
      <h4 class="text-xl md:text-2xl">
        <strong>{{ count }}</strong>
        <small>{{ unit }}</small>
      </h4>
    </section>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      default: ''
    },
    count: {
      type: Number,
      default: 0
    },
    unit: {
      type: String,
      default: '-'
    }
  }
}
</script>

<style>

</style>
