<template>
    <div class="main-header-list">
        <slot />
    </div>
</template>

<style>
.main-header-list {
    > ul {
        display: flex;
        flex-direction: column;
        justify-content: space-evenly;
        align-items: stretch;
        list-style-type: none !important;
        height: 100%;

        > li {
            margin-left: 0;
            padding-left: 0;

            > ul {
                padding-top: 18px;
                padding-left: 50px;
                border: 1px solid;
                border-radius: 8px;
                @apply text-sm
            }

            > span {
                display: block;
                position: relative;
                font-weight: 700;
                font-style: italic;
                border-radius: 8px;
                top: 20px;
                left: 45px;
                width: 60%;
                padding: 5px 10px;
            }

            &:nth-child(1) {
                > ul {
                    border-color: var(--slidev-theme-variant1);
                }

                > span {
                    background-color: var(--slidev-theme-variant1);
                }
            }

            &:nth-child(2) {
                > ul {
                    border-color: var(--slidev-theme-variant2);
                }

                > span {
                    background-color: var(--slidev-theme-variant2);
                }
            }

            &:nth-child(3) {
                > ul {
                    border-color: var(--slidev-theme-variant3);
                }

                > span {
                    background-color: var(--slidev-theme-variant3);
                }
            }
        }
    }
}
</style>