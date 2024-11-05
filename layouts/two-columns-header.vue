<template>
  <div class="slidev-layout two-columns-header">
    <slot/>
    <div class="two-columns">
      <slot name="left"/>
      <slot name="right"/>
    </div>
  </div>
</template>

<style>
.two-columns-header {
  display: flex;
  flex-direction: column;

  > h1 {
    flex: 0 0;
  }

  > .two-columns {
    flex: 1 1;
    display: flex;
    flex-direction: row !important;
    align-items: center;
    justify-content: space-between;
  }
}
</style>