<template>
  <div class="grouped-list">
    <slot/>
  </div>
</template>

<style>
div.grouped-list {
  display: flex;
  justify-content: center !important;

  > ul {
    display: flex;
    list-style: none;
    justify-content: space-between;
    align-items: stretch;
    gap: 50px;
    height: 100%;

    > li {
      @apply line-height-tight;
      flex: 1 1;
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;
      margin-left: 0;
      padding: 30px 20px 20px 20px;
      border: 1px solid var(--slidev-theme-primary);
      background-color: rgba(var(--slidev-theme-primaryLightRGB), 0.3);
      border-radius: 15px;

      > strong {
        @apply text-2xl;
        flex: 1 1;
      }

      > ul {
        flex: 5 5;
        display: flex;
        justify-content: space-around;
        flex-direction: column;
        gap: 10px;
        padding: 0;
        margin: 0;
        list-style: none;
        width: 100%;
        align-items: center;

        > li {
          margin-left: 0;
          border: 1px solid white;
          background-color: rgba(var(--slidev-theme-primaryRGB), 0.9);
          border-radius: 15px;
          padding: 15px;
          height: 100%;
          display: flex;
          align-items: center;
          text-align: center;
          flex: 1 1;
        }
      }
    }
  }
}
</style>