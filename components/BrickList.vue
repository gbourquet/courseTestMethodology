<template>
    <div class="brick-list">
        <slot />
    </div>
</template>

<style>
.brick-list {
    ul {
        list-style-type: none !important;

        li {
            margin: 0;
        }
    }

    > ul {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-auto-rows: 1fr;
        gap: 50px;
        height: 100%;
        align-items: center;
        justify-items: center;

        > li {
            line-height: normal;
            padding: 20px 15px;
            text-align: center;
            background-color: red;
            height: 100%;
            width: 100%;
            display: grid;
            align-content: center;

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

}

</style>