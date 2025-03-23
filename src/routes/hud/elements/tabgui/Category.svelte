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

    /*.name {
        font-weight: 500;
        color: $tabgui-text-color;
        font-size: 14px;
        width: 100%;
        padding: 7px 11px 7px 11px;

        background: linear-gradient(
            to left,
            rgba(0, 0, 0, 0.5) 50%,
            $tabgui-selected-color 50%
        );
        background-size: 200% 100%;
        background-position: right bottom;
        will-change: background-position;
        overflow: hidden;
    }

    .category {
        display: flex;

        &.selected .name {
            background-position: left bottom;
        }

        &.selected .arrow {
            background-position: left bottom;
        }
    }

    .arrow {
        background: linear-gradient(
            to left,
            rgba(0, 0, 0, 0.5) 50%,
            $tabgui-selected-color 50%
        );
        background-size: 200% 100%;
        background-position: right bottom;
        will-change: background-position;
        overflow: hidden;

        text-align: center;
        color: $tabgui-text-color;
        font-weight: 500;
        font-size: 14px;
        width: 40px;
        padding: 7px 12px 7px 12px;
    }*/

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
