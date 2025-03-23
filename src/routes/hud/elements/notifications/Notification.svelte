<script lang="ts">
    export let text: string;
</script>

<div class="notification">
    <div class="message">{text}</div>
</div>

<style lang="scss">
    @use "../../../../colors.scss" as *;

    .notification {
        column-gap: 10px;
        background: rgba(0, 0, 0, 1.0);
        width: 200px;
        overflow: hidden;
        padding: 10px;
        margin-bottom: 10px;
        border-left: solid 5px $notification-border-color;
    }

    .message {
        font-size: 14px;
        color: #6b6c6e;
    }
</style>
