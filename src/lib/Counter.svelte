<script lang="ts">
    import {invoke} from '@tauri-apps/api/core';

    let count: number = $state(0)
    const increment = async () => {
        count = await invoke('my_custom_command', {arg: count});
    }
</script>

<button onclick={increment}>
    count is {count}
</button>
