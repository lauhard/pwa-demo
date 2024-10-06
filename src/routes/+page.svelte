<script lang="ts">
</script>

<section>
    <h1>Codepad</h1>
    <form action="">
        <textarea name="" id=""> </textarea>
        <ul>
            <li>
                <button type="submit">
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
    <ul id="notes"></ul>
</section>

<style lang="scss">
    ul {
        list-style: none;
        padding: 0;
        text-align: center;
        display: flex;
        margin: 5px;
    }

    form {
        margin: 16px;
        text-align: center;
    }
    #notes {
        flex-flow: column;
        flex-wrap: nowrap;
        align-items: stretch;
        align-content: center;
        justify-content: space-evenly;
        padding-bottom: 50px;
        color: var(--color-text);
    }

    #notes li {
        margin-bottom: 16px;
        border-top: 2px dotted var(--color-title-back);
        padding-top: 8px;
    }

    #toolbar {
        flex-wrap: wrap;
        align-items: stretch;
        align-content: center;
        justify-content: space-evenly;
    }

    section > #toolbar {
        position: fixed;
        bottom: 0;
        margin: 0;
        width: 100%;
        background-color: var(--color-toolbar);
    }

    @media (display-mode: standalone), (display-mode: minimal-ui) {
        body > #toolbar {
            padding: env(safe-area-inset-top) env(safe-area-inset-right)
                env(safe-area-inset-bottom) env(safe-area-inset-left) !important;
        }

        #itemInstall {
            display: none;
        }
    }
</style>
