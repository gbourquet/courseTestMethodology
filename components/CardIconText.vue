<template>
    <div class="card-icon-text">
        <slot />
    </div>
</template>
<script setup lang="ts">
</script>

<style>
.card-icon-text {
    display: flex;
    align-items: center;

    > ul {
        list-style-type: none;
        display: flex;
        flex-wrap: wrap;
        align-items: flex-start;
        justify-content: center;
        row-gap: 50px;
        column-gap: 5%;

        > li {
            @apply line-height-tight;
            @apply text-sm;
            width: 30%;
            margin: 0;
            padding: 0 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            text-align: center;

            > span {
                @apply font-bold;
                @apply text-xl;
            }

            > svg {
                @apply text-8xl;
            }

            &:nth-child(1) > svg {
                color: var(--slidev-theme-primary);
            }

            &:nth-child(1) > svg {
                color: var(--slidev-theme-primary);
            }

            &:nth-child(2) > svg {
                color: var(--slidev-theme-variant1);
            }

            &:nth-child(3) > svg {
                color: var(--slidev-theme-variant2);
            }

            &:nth-child(4) > svg {
                color: var(--slidev-theme-variant3);
            }

            &:nth-child(5) > svg {
                color: var(--slidev-theme-variant4);
            }

            &:nth-child(6) > svg {
                color: var(--slidev-theme-variant5);
            }
        }
    }

}
</style>