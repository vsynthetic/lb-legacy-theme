<script lang="ts">
    import { onDestroy } from "svelte";
    import { flip } from "svelte/animate";
    import { listen } from "../../../../integration/ws";
    import { fly } from "svelte/transition";
    import Notification from "./Notification.svelte";
    import type { NotificationEvent } from "../../../../integration/events";

    interface TNotification {
        animationKey: number;
        id: number;
        text: string;
        time: number;
    }

    let notifications: TNotification[] = [];
    let backbuffer: TNotification[] = [];

    let lastPollTime: number = 0;

    function poll(): TNotification[] {
        if (backbuffer.length === 0) return [];
        const head = backbuffer.pop();
        if (head === undefined) return [];
        lastPollTime = Date.now();
        head.time = Date.now();
        return [head];
    }

    function addNotification(text: string) {
        let animationKey = Date.now();
        const id = animationKey;

        backbuffer = [{ animationKey, id, text, time: 0 }, ...backbuffer];
    }

    function pollNotification() {
        if (notifications.length === 0) {
            if (Date.now() - lastPollTime > 1000)
                notifications = poll();
        } else if (
            Date.now() - notifications[0].time >
            50 * notifications[0].text.length
        ) {
            notifications = [];
        }
    }

    const intervalId = setInterval(pollNotification, 10);

    onDestroy(() => {
        clearInterval(intervalId);
    });

    listen("notification", (e: NotificationEvent) => {
        if (e.severity === "ENABLED" || e.severity == "DISABLED") {
            addNotification(`${e.title} ${e.message}`);
        } else {
            addNotification(e.message);
        }
    });
</script>

<div class="notifications">
    {#each notifications as { text, animationKey } (animationKey)}
        <div
            animate:flip={{ duration: 200 }}
            in:fly={{ x: 30, duration: 200 }}
            out:fly={{ x: 30, duration: 200 }}
        >
            <Notification {text} />
        </div>
    {/each}
</div>
