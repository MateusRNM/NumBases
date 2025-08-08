<script>
    import { bases } from "$lib/data";
    let from = $state(10);
    let to = $state(2);
    let input = $state('');
    let error = $state('');
    let minNum = $state(0);
    let maxNum = $state(100);
    let desafio = $state('');
    let resposta = $state('');
    let resultado = $state(null);

    function gerar() {
        error = "";
        if (from == to) {
            error = "As bases de origem e destino devem ser diferentes!";
            return;
        }
        input = "";
        resultado = null;
        let randomNumber = Math.floor(Math.random() * (maxNum - minNum + 1)) + minNum;
        desafio = randomNumber.toString(from).toUpperCase();
        resposta = randomNumber.toString(to).toLowerCase();
    }

    function reset() {
        input = "";
        desafio = "";
        resposta = "";
        resultado = null;
        error = "";
    }

    function verificar() {
        if (input === "") return;
        resultado = input.toLowerCase() === resposta;
        setTimeout(() => {
            if (resultado) {
                gerar(); 
            }
            resultado = null;
        }, 3000);
    }
</script>

<main class="container py-4 py-lg-5">
    
    <div class="row g-4 justify-content-center">
        <div class="col-lg-5 col-md-10">
            <div class="card h-100 shadow-sm">
                <div class="card-header">
                    <h5 class="mb-0">Configurações</h5>
                </div>
                <div class="card-body d-flex flex-column">
                    <div class="row g-3">
                        <div class="col-6">
                            <label for="fromBase" class="form-label">Converter de:</label>
                            <select id="fromBase" class="form-select" bind:value={from} onchange={reset}>
                                {#each bases as base}
                                    <option value={base.value}>{base.nome}</option>
                                {/each}
                            </select>
                        </div>
                        <div class="col-6">
                            <label for="toBase" class="form-label">Para:</label>
                            <select id="toBase" class="form-select" bind:value={to} onchange={reset}>
                                {#each bases as base}
                                    <option value={base.value}>{base.nome}</option>
                                {/each}
                            </select>
                        </div>

                        <div class="col-6">
                             <label for="minNum" class="form-label">Nº Mínimo (Decimal)</label>
                             <input id="minNum" type="numeric" class="form-control text-center" bind:value={minNum}>
                        </div>
                         <div class="col-6">
                             <label for="maxNum" class="form-label">Nº Máximo (Decimal)</label>
                             <input id="maxNum" type="numeric" class="form-control text-center" bind:value={maxNum}>
                        </div>
                    </div>

                    <div class="mt-auto pt-4 text-center">
                        {#if error}
                            <div class="alert alert-danger small p-2">{error}</div>
                        {/if}
                        <button class="btn btn-primary w-100" onclick={gerar}>
                            Gerar Novo Desafio
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <div class="col-lg-7 col-md-10">
            <div class="card h-100 shadow-sm">
                <div class="card-header">
                    <h5 class="mb-0">Desafio</h5>
                </div>
                <div class="card-body d-flex flex-column justify-content-center text-center p-4">
                    {#if !desafio}
                        <div class="text-muted">
                             <p class="fs-4">Aguardando desafio...</p>
                        </div>
                    {:else}
                        <p class="text-muted mb-2">Converta o número abaixo:</p>
                        <h2 class="display-5 fw-bold text-primary mb-4">
                            ({desafio})<sub class="fs-5 align-baseline ms-1">{from}</sub> = (?)<sub class="fs-5 align-baseline ms-1">{to}</sub>
                        </h2>
                        
                        <div class="input-group mb-3 mx-auto" style="max-width: 350px;">
                            <input 
                                type="text" 
                                class="form-control form-control-lg text-center" 
                                placeholder="Sua resposta"
                                bind:value={input}
                                onkeydown={(e) => e.key === 'Enter' && verificar()}
                            >
                            <button class="btn btn-success" onclick={verificar}>Verificar</button>
                        </div>

                        {#if resultado !== null}
                             <div class="alert {resultado ? 'alert-success' : 'alert-danger'} mt-3 mx-auto" style="max-width: 350px;">
                                {resultado ? 'Parabéns, você acertou!' : 'Resposta incorreta. Tente de novo!'}
                             </div>
                        {/if}
                    {/if}
                </div>
            </div>
        </div>

    </div>
</main>