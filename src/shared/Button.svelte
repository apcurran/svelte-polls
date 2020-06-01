<script>
    export let type = "primary";
    export let flat = false;
    export let inverse = false;
</script>

<button class={type} class:flat={flat} class:inverse={inverse}>
    <slot></slot>
</button>

<style>
    button {
        border: none;
        cursor: pointer;
        font-weight: bold;
        border-radius: 4px;
        padding: .75rem 1.35rem;
        box-shadow: 1px 2px 3px rgba(0, 0, 0, .2);

        --red: #d91b42;
        --green: #45c496;
    }

    .primary {
        background-color: var(--red);
        color: #fff;
    }

    .secondary {
        background-color: var(--green);
        color: #fff;
    }

    .flat {
        box-shadow: none;
    }

    .primary.inverse {
        color: var(--red);
        background-color: #fff;
        border: 2px solid var(--red);
    }

    .secondary.inverse {
        color: var(--green);
        background-color: #fff;
        border: 2px solid var(--green);
    }
</style>