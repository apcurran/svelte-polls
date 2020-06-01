<script>
    import { createEventDispatcher } from "svelte";
    const dispatch = createEventDispatcher();

    export let items;
    export let activeItem;
</script>

<div class="tabs">
    <ul>
        {#each items as item}
            <li on:click={() => dispatch("tabChange", item)}>
                <p class:active={item === activeItem}>{item}</p>
            </li>
        {/each}
    </ul>
</div>

<style>
    .tabs {
        margin-bottom: 3rem;
    }

    ul {
        display: flex;
        justify-content: center;
        list-style: none;
    }

    li {
        margin: 0 1rem;
        font-size: 1.2rem;
        color: #444;
        cursor: pointer;
    }

    .active {
        color: #d91b42;
        border-bottom: 2px solid #d91b42;
        padding-bottom: .75rem;
    }
</style>