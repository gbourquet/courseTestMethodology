<template>
  <div class="process-list">
    <slot/>
  </div>
</template>

<style>
div.process-list {
  display: flex;
  justify-content: center !important;
  height: 100%;

  ul {
    list-style: none;

    li {
      margin-left: 0;
      padding-left: 0;
    }
  }

  > ul {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    gap: 60px;

    > li {
      display: flex;
      flex: 1 1;

      &:nth-child(1) {
        > strong {
          background-color: var(--slidev-theme-variant1);
        }

        > ul {
          background-color: rgba(var(--slidev-theme-variant1RGB), 0.5);
        }
      }

      &:nth-child(2) {
        > strong {
          background-color: var(--slidev-theme-variant2);
        }

        > ul {
          background-color: rgba(var(--slidev-theme-variant2RGB), 0.5);
        }
      }

      &:nth-child(3) {
        > strong {
          background-color: var(--slidev-theme-variant3);
        }

        > ul {
          background-color: rgba(var(--slidev-theme-variant3RGB), 0.5);
        }
      }

      > strong {
        @apply text-sm text-center;
        display: flex;
        flex-direction: column;
        flex: 2 2;
        justify-content: center;
      }

      > ul {
        flex: 5 5;
        display: flex;
        flex-direction: column;
        justify-content: center;
        padding-left: 10px;

        > li {
          @apply text-xs;
        }
      }
    }
  }
}
</style>