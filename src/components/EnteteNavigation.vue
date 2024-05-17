<template>
    <header>
        <div class="container">
            <div class="title">
                <h1 class="green-title">Le Panier Vert</h1>
                <p>La boutique en ligne des choses qui sont vertes.</p>
            </div>
            <div class="nav">
                <!-- ** Exercice 3: faire en sorte que la navigation ne recharge pas la page ** -->
                <a href="/">Achats</a> | 
                <a href="/checkout">Caisse</a>
            </div>
            <div class="panier">
                <!-- ** Exercice 5: afficher le nombre d'articles et le coût total du panier ** -->
                <div>Panier : N articles</div>
                <div>Total : NN,NN$</div>
            </div>
        </div>
    </header>
</template>

<script>
import { formatCurrency } from '../text_format';

export default {
}
</script>

<style scoped>
.green-title {
    color: green;
}

.container {
    display: flex;
    justify-content: space-between;
    padding: 0rem;
}

.title {
    flex-basis: 30%;
    padding: 0.3rem;
}

.nav {
    flex-basis: 55%;
    padding: 0.3rem;
}

.panier {
    flex-basis: 15%;
    padding: 0.3rem;
}
</style>
