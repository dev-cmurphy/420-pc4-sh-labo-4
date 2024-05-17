<template>
    <div class="boxed-left">
        <form @submit.prevent="soumettreInfos">
            <div>
                <h2>Paiement</h2>
                <div class="form-control" :class="{ invalide: !nomPaiementValide }">
                    <label for="nom-paiement">Nom sur la carte de crédit: </label>
                    <!-- L'événement blur survient lorsqu'on perd le focus de ce champ -->
                    <!-- Le modificateur .trim ajouté à v-model supprime les espaces au début et à la fin de la chaîne entrée -->
                    <input id="nom-paiement" name="nom-paiement" type="text" v-model.trim="nomPaiement"
                        @blur="validerNomPaiement" />
                    <span v-if="!nomPaiementValide">Veuillez entrer un nom !</span>
                </div>
                <div class="form-control" :class="{ invalide: !carteCreditValide }">
                    <label for="cartecredit">Numéro de carte de crédit: </label>
                    <input id="cartecredit" name="cartecredit" type="text" v-model.trim="carteCredit" />
                    <span v-if="!carteCreditValide">Veuillez entrer un numéro de carte de crédit sous la forme 4555 5555
                        5555 5555</span>
                </div>
                <!-- ** Exercice 4.1 : ajouter le nécessaire pour que les champs soient validés et pour afficher les erreurs
                     de validation ** -->
                <div class="form-control">
                    <label for="dateexp">Année et mois d'expiration (AAAA/MM): </label>
                    <input id="dateexp" name="dateexp" type="text" v-model.trim="dateExp" />
                </div>
            </div>
            <h2>Expédition</h2>
            <div>
                <h4>Mode d'expédition</h4>
                <div class="form-control">
                    <input id="expedition-postes-canada" name="expedition" type="radio" value="postescanada"
                        v-model="modeExpedition" />
                    <label for="expedition-postes-canada">Postes Canada</label>
                    <input id="expedition-purolator" name="expedition" type="radio" value="purolator"
                        v-model="modeExpedition" />
                    <label for="expedition-purolator">Purolator</label>
                    <input id="expedition-fedex" name="expedition" type="radio" value="fedex" v-model="modeExpedition" />
                    <label for="expedition-fedex">FedEx</label>
                </div>
            </div>
            <div>
                <h4>Adresse</h4>
                <div class="form-control">
                    <label for="nom-expedition">Nom: </label>
                    <input id="nom-expedition" name="nom-expedition" type="text" v-model.trim="nomExpedition" />
                </div>
                <div class="form-control">
                    <label for="adresse-expedition">Adresse: </label>
                    <input id="adresse-expedition" name="adresse-expedition" type="text" v-model.trim="adresse" />
                </div>
                <div class="form-control">
                    <label for="ville-expedition">Ville: </label>
                    <input id="ville-expedition" name="ville-expedition" type="text" v-model.trim="ville" />
                </div>
                <div class="form-control">
                    <label for="province">Province: </label>
                    <select id="province" name="province">
                        <option v-for="province in listeProvinces" :value="province">{{ province }}</option>
                    </select>
                </div>
                <div class="form-control">
                    <label for="codepostal-expedition">Code postal: </label>
                    <input id="codepostal-expedition" name="codepostal-expedition" type="text" v-model.trim="codePostal" />
                </div>
            </div>
            <button>Passer la commande</button>
        </form>
    </div>
</template>

<script>

export default {
    data() {
        return {
            nomPaiement: '',
            nomPaiementValide: true,
            carteCredit: '',
            carteCreditValide: true,
            dateExp: '',
            // ** Exercice 4.1 : ajouter des propriétés booléenes au besoin pour les résultats de validation **
            modeExpedition: 'postescanada',
            nomExpedition: '',
            adresse: '',
            ville: '',
            province: '',
            listeProvinces:
                [
                    'Yukon',
                    'Territoires du Nord-Ouest',
                    'Nunavut',
                    'Colombie-Britannique',
                    'Alberta',
                    'Saskatchewan',
                    'Manitoba',
                    'Ontario',
                    'Québec',
                    'Nouveau-Brunswick',
                    'Nouvelle-Écosse',
                    'Île-du-Prince-Édouard',
                    'Terre-Neuve et Labrador'
                ],
            codePostal: ''
        }
    },
    methods: {
        soumettreInfos() {
            console.log('nomPaiement: ', this.nomPaiement);
            console.log('carteCredit: ', this.carteCredit);
            console.log('dateExp: ', this.dateExp);
            console.log('modeExpedition: ', this.modeExpedition);
            console.log('nomExpedition: ', this.nomExpedition);
            console.log('adresse: ', this.adresse);
            console.log('ville: ', this.ville);
            console.log('province: ', this.province);
            console.log('nomPaiement: ', this.nomPaiement);
            console.log('codePostal: ', this.codePostal);

            // ** Exercice 4.2 : ajouter les validations pour soumission du formulaire ici
            // et empêcher de réinitialiser le formulaire et le panier s'il y a une erreur quelconque **
            this.validerNomPaiement();
            this.validerCarteCredit();

            if (this.nomPaiementValide && this.carteCreditValide) {
                alert("Merci d'avoir commandé au Panier Vert!");
                this.reinitialiserFormulaire();
                this.reinitialiserPanier();
            } else {
                alert("Veuillez corriger les informations erronées");
            }
        },
        reinitialiserFormulaire() {
            // ** Exercice 4.2 : ajouter ce qu'il faut pour réinitialiser les nouveaux champs pour les résultats de validation **
            this.nomPaiement = '';
            this.nomPaiementValide = true;
            this.carteCredit = '';
            this.carteCreditValide = true;
            this.dateExp = '';
            this.modeExpedition = 'postescanada';
            this.nomExpedition = '';
            this.adresse = '';
            this.ville = '';
            this.province = '';
        },
        reinitialiserPanier() {
            // ** Exercice 4.3 : ajouter la logique pour vider tout le panier **
        },
        validerNomPaiement() {
            if (this.nomPaiement === '') {
                this.nomPaiementValide = false;
            } else {
                this.nomPaiementValide = true;
            }
        },
        validerCarteCredit() {
            const regex = /4[0-9]{3}(?: [0-9]{4}){3}/;
            if (this.carteCredit && regex.test(this.carteCredit)) {
                this.carteCreditValide = true;
            } else {
                this.carteCreditValide = false;
            }
        }
        // ** Exercice 4.1 : ajouter les méthodes de validation nécessaires **
        // Informations utiles :
        // regex pour valider le mois et année (AAAA/MM) : /[0-9]{4}\/[0-1][0-9]/
        // (permet d'entrer des mois plus grands que 12 mais bon ...)
        // 
        // regex pour valider le code postal : /[ABCEGHJKLMNPRSTVXY][0-9][ABCEGHJKLMNPRSTVWXYZ] ?[0-9][ABCEGHJKLMNPRSTVWXYZ][0-9]/
    },
    watch: {
        carteCredit(nouvCarteCredit) {
            this.validerCarteCredit();
        }
        // ** Exercice 4.1 : ajouter les watch nécessaires pour les validations
        // (une alternative est d'utiliser v-on, p.ex. avec l'événement blur) **
    }
}
</script>

<style scoped>
.form-control.invalide input,
.form-control.invalide select {
    border-color: red;
}

.form-control.invalide label {
    color: red;
}

form * {
    margin: 0.3rem;
}

.boxed-left {
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    margin: 1rem auto;
    border-radius: 10px;
    padding: 1rem;
    text-align: left;
    width: 90%;
    max-width: 80rem;
}
</style>
