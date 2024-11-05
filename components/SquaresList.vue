<template>
  <div class="squares-list">
    <slot/>
  </div>
</template>

<style>
div.squares-list {
  display: flex;
  flex-direction: column;
  justify-content: center !important;
}

div.squares-list > ul {
  display: flex;
  list-style: none;
  justify-content: space-between;
  align-items: stretch;
  gap: 50px;

  > li {
    @apply line-height-tight;
    flex: 1 1;
    display: flex;
    align-items: center;
    text-align: center;
    margin-left: 0;
    padding: 10px;
    border: 1px solid var(--slidev-theme-primary);
    background-color: rgba(var(--slidev-theme-primaryLightRGB), 0.3);
    border-radius: 15px;
    box-shadow: -15px -15px var(--slidev-theme-primary)
  }
}
</style>