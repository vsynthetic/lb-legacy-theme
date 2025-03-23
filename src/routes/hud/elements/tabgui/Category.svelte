<script lang="ts">
    import { fade } from "svelte/transition";

    export let name: string;
    export let selected: boolean;
</script>

<div class="category" class:selected>
    <div class="name">
        {name}
    </div>
    <div class="arrow">></div>
</div>

<style lang="scss">
    @use "../../../../colors.scss" as *;

    .category {
        display: flex;
        justify-content: space-between; // This moves the arrow to the far right
        align-items: center; // This centers the text vertically)
        background: rgba(0, 0, 0, 0.5);
        color: $tabgui-text-color;
        text-shadow: 2px 2px $tabgui-text-shadow;
        font-weight: 500;
        font-size: 14px;
        height: 25px;
        width: 100px;
        padding: 2px 4px;

        &.selected {
            background-color: $tabgui-selected-color;
        }
    }

    .name {
        margin-right: 5px;
    }

    .arrow {
        padding-right: 5px;
    }
</style>
