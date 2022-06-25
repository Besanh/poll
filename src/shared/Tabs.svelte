<script>
    import { createEventDispatcher } from "svelte";

    const dispatch = createEventDispatcher();
    let activeItem;
    let items;

    export { activeItem, items };
</script>

<div class="tabs">
    <ul>
        {#each items as item (item.id)}
            <li
                on:click={() => {
                    dispatch("tabChange", item);
                }}
            >
                <div class:active={item.name === activeItem}>
                    {item.name}
                </div>
            </li>
        {/each}
    </ul>
</div>

<style>
    .tabs {
        margin-bottom: 40px;
    }
    ul {
        display: flex;
        justify-content: center;
        padding: 0;
        list-style-type: none;
    }
    li {
        margin: 0 16px;
        font-size: 18px;
        color: #555;
        cursor: pointer;
    }
    .active {
        color: #d91b42;
        border-bottom: 2px solid #d91b42;
        padding-bottom: 8px;
    }
</style>
