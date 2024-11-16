<template>
    <div class="slidev-layout two-columns-header">
        <slot />
        <div class="two-columns">
            <div>
                <slot name="left" />
            </div>
            <div>
                <slot name="right" />
            </div>
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
        gap: 30px;

        > div {
            flex: 1 1;
        }
    }
}
</style>
<script setup lang="ts">
</script>