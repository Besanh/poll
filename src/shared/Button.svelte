<script>
    let type_btn = "primary";
    let flat = false;
    let inverse = false;
    $: class_name = `${type_btn}`;
    export { type_btn, flat, inverse };
</script>

<button class={class_name} class:flat class:inverse>
    <slot />
</button>

<style>
    button {
        border: 0;
        cursor: pointer;
        border-radius: 5px;
        padding: 8px 12px;
        font-weight: bold;
        box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.2);
    }
    .primary {
        background: #4424b6;
        color: white;
    }
    .secondary {
        background: #45c496;
        color: white;
    }
    .flat {
        box-shadow: none;
    }
    .primary.inverse {
        color: #4424b6;
        background: white;
        border: 1px solid #4424b6;
    }
    .secondary.inverse {
        color: #45c496;
        background: white;
        border: 1px solid #45c496;
    }
</style>
