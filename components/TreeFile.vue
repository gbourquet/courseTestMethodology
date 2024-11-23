<template>
    <div class="tree-file">
        <slot />
    </div>
</template>
<script setup lang="ts">
</script>

<style>
.tree-file {
    @apply text-xs;
    padding-bottom: 10px;

    .fa-folder-open, .fa-folder {
        color: #007bff;
    }

    .fa-html5 {
        color: #f21f10;
    }

    ul {
        padding-left: 5px;
        list-style: none;

        li {
            position: relative;
            padding-left: 10px;
            -webkit-box-sizing: border-box;
            -moz-box-sizing: border-box;
            box-sizing: border-box;

            &:before {
                position: absolute;
                top: 11px;
                left: 0;
                width: 7px;
                height: 1px;
                margin: auto;
                content: '';
                background-color: #666;
            }

            &:after {
                position: absolute;
                top: 0;
                bottom: 0;
                left: 0;
                width: 1px;
                height: 100%;
                content: '';
                background-color: #666;
            }

            &:last-child:after {
                height: 11px;
            }

            svg {
                color: var(--slidev-theme-primary);
            }
        }
    }
}
</style>