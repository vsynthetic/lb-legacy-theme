<script lang="ts">
    import {afterUpdate} from "svelte";
    import {setModuleEnabled} from "../../../../integration/rest";
    import {convertToSpacedString, spaceSeperatedNames} from "../../../../theme/theme_config";

    export let name: string;
    export let enabled: boolean;
    export let selected: boolean;

    let moduleElement: HTMLElement;

    afterUpdate(() => {
        if (moduleElement && selected) {
            moduleElement.scrollIntoView({
                behavior: "smooth",
                block: "nearest",
            });
        }
    });

    async function handleKeyDown(e: KeyboardEvent) {
        if (selected && e.key === "Enter") {
            await setModuleEnabled(name, !enabled);
        }
    }
</script>

<svelte:window on:keydown={handleKeyDown} />

<div class="module" class:enabled class:selected bind:this={moduleElement}>
    <div class="name">{$spaceSeperatedNames ? convertToSpacedString(name) : name}</div>
</div>

<style lang="scss">
    @use "../../../../colors.scss" as *;

    .module {
        font-weight: 500;
        color: $tabgui-text-dimmed-color;
        font-size: 14px;
        padding: 6px 15px 6px 10px;
        background-color: rgba(0, 0, 0, 0.5);

        &.selected {
            background-color: $tabgui-selected-color;
        }

        &.enabled {
            color: $tabgui-text-color;
        }
    }
</style>
