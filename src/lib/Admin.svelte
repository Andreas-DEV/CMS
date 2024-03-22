<script async lang="ts">
    import { pb, currentUser } from "../lib/pocketbase";
    import PocketBase from "pocketbase";

    const pbConnect = new PocketBase("http://127.0.0.1:8090");

    function logUd() {
        pb.authStore.clear();
    }

    let errMsg: string = "";

    let textData: string;

    let nyhedsId: string = "";

    async function submitData() {
        try {
            const create = await pbConnect
                .collection("nyheder")
                .create({ text: textData });

            errMsg = "Request submitted succesfully.";
        } catch (err: any) {
            errMsg = err;
        }
    }

    let updateMsg = "";
    async function updateData() {
        const data = {
            text: "jeg er opdateret",
        };

        try {
            const record = await pb
                .collection("nyheder")
                .update(nyhedsId, {text: textData});

            updateMsg = "opdateret korrekt!";
        } catch (err) {
            updateMsg = err;
        }
    }
</script>

<!-- HTML KODE -->

<main class="mainContainer">
    <aside class="adminPanel">
        <button class="adminBtn" on:click={logUd}>Log ud</button>
    </aside>
    <section class="adminContent">
        <form on:submit|preventDefault>
            <p>{errMsg}</p>
            <div class="testUsers">
                <input type="text" name="" id="" placeholder="Put ID her..." bind:value={nyhedsId}>
                <button on:click={updateData}>Update</button>
                <button class="submitBtn" on:click={submitData}>Opret</button>
                <p class="hr"></p>
                <textarea name="" id="" cols="34" rows="10" bind:value={textData} placeholder="Input data her..."/>
                <p>Response: {updateMsg}</p>
            </div>
        </form>
    </section>
</main>

<style lang="scss">
    @import url("https://fonts.googleapis.com/css2?family=Noto+Sans+Khojki&family=Quicksand:wght@300;600;700&display=swap");

    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    .hr {
        
        width: 2%;
        margin: .5rem auto;
    }

    .mainContainer {
        display: flex;
        gap: 1rem;

        align-items: center;

        .adminContent {
            padding: 1rem;
        }

        .adminBtn {
            padding: 0.3rem 0.5rem;
            position: absolute;
            bottom: 5px;
            left: 5px;
        }
    }

    /* .mainContainer {
        position: absolute;
        padding: 0;
        margin: 0;
        display: flex;
        width: 100%;

        .adminPanel {
            

            width: 300px;
            height: 1500px;
            background-color: #333;
            
            .adminBtn {
                
            }
        }
    } */
</style>
