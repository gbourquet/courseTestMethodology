<template>
    <div class="slidev-layout content-vertical-center">
        <slot />
    </div>
</template>

<style>
.content-vertical-center {
    display: flex;
    flex-direction: column;

    > h1 {
        flex: 0 0;
    }

    > * {
        flex: 1 1;
    }
}

</style>