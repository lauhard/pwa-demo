<script lang="ts">
    interface Item {
        id: string;
        content: string;
    }

    import { enhance } from "$app/forms";

    let form: HTMLFormElement;
    let texareaInput: string = $state("");
    let items: Item[] = $state([]);
    let acive: boolean = $state(false);
    $effect(() => {});
    const pushToList = (e: Event) => {
        e.preventDefault();
        if (texareaInput.trim() === "") return;
        items = [...items, { id: crypto.randomUUID(), content: texareaInput }];
        texareaInput = "";
    };

    const deleteItem = (id: string) => {
        items = items.filter((item) => item.id !== id);
    };
</script>

<section>
    <h1>Codepad1</h1>
    <form bind:this={form} action="" use:enhance method="post">
        <textarea bind:value={texareaInput} name="" id=""> </textarea>
        <ul>
            <li>
                <button type="submit" onclick={pushToList}>
                    <span class="icon"> save </span>
                    Save
                </button>
            </li>
        </ul>
    </form>
    <ul id="toolbar">
        <li>
            <button>
                <span class="icon"> school </span>
                Learn
            </button>
        </li>
        <li>
            <button>
                <span class="icon"> share </span>
                Share
            </button>
        </li>
        <li>
            <button>
                <span class="icon"> download </span>
                Install
            </button>
        </li>
    </ul>

    <ul id="notes">
        {#each items as item, i}
            <li class="item">
                <p>
                    {item.content}
                </p>
                <button class="btn-del" onclick={() => deleteItem(item.id)}>
                    <span class="icon"> delete </span>
                    Delete
                </button>
            </li>
        {:else}
            <li>
                <p>No notes yet</p>
            </li>
        {/each}
    </ul>
</section>

<style lang="scss">
    section {
        display: flex;
        flex-direction: column;
        background-color: var(--color-back);
        color: var(--color-text);
    }
    ul {
        list-style: none;
        padding: 0;
        text-align: center;
        display: flex;
        margin: 5px;
    }

    form {
        display: flex;
        flex-direction: column;
        justify-content: center;
        margin-block: 2rem;
        width: 100%;

        ul {
            li {
                display: flex;
                justify-content: center;
                width: 100%;
                align-items: center;
                border-radius: 10px;
            }
        }
    }

    #notes {
        flex-flow: column;
        color: var(--color-text);
        max-height: 400px;
        overflow-y: auto;
        width: 90vw;
        min-width: 300px;
        height: 100%;
        display: flex;
        justify-self: center;
        align-self: center;

        li {
            border-top: 2px dotted var(--color-title-back);
            display: flex;
            width: 100%;
            height: 100%;
            justify-content: space-between;
            align-items: center;

            p {
                word-break: unset;
                line-break: normal;
                white-space: pre-wrap;
                height: 100%;
                width: inherit;

                text-align: left;
                justify-content: space-between;

                overflow: hidden;
                overflow-y: auto;
                //white-space: nowrap;
                //text-overflow: ellipsis;
                max-height: 50px;
                height: 100%;
            }
            .btn-del {
                height: 40px;
                width: 100px;
            }
        }
    }
    section {
        #toolbar {
            flex-wrap: wrap;
            align-items: stretch;
            align-content: center;
            justify-content: space-evenly;
            position: fixed;
            bottom: 0;
            margin: 0;
            width: 100%;
            background-color: var(--color-toolbar);
        }
    }

    @media (display-mode: standalone), (display-mode: minimal-ui) {
        section {
            #toolbar {
                padding: env(safe-area-inset-top) env(safe-area-inset-right)
                    env(safe-area-inset-bottom) env(safe-area-inset-left) !important;
            }
        }

        #itemInstall {
            display: none;
        }
    }
</style>
