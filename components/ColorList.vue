<template>
  <div class="color-list">
    <slot/>
  </div>
</template>

<style>
.color-list ul {
  list-style-type: none !important;
}

.color-list > ul {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;

  > li {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
    margin-left: 0;
    flex: 1 1;
    border-radius: 10px;

    > svg {
      @apply text-4xl;
    }

    > span {
      @apply text-xl;
    }

    :nth-child(1) {
      flex: 1 1;
    }

    :nth-child(2) {
      flex: 4 4;
    }

    :nth-child(3) {
      @apply text-sm;
      flex: 4 4;
      flex-direction: column;
    }

    &:nth-child(1) {
      background-color: var(--slidev-theme-primary);
    }

    &:nth-child(2) {
      background-color: var(--slidev-theme-variant1);
    }

    &:nth-child(3) {
      background-color: var(--slidev-theme-variant2);
    }

    &:nth-child(4) {
      background-color: var(--slidev-theme-variant3);
    }

    &:nth-child(5) {
      background-color: var(--slidev-theme-variant4);
    }

    &:nth-child(6) {
      background-color: var(--slidev-theme-variant5);
    }
  }
}

</style>