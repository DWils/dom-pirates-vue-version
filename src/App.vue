<template>
  <div id="game-body">
    <div id="container">
      <!-- Zone de jeu : la mer -->
      <div id="map">
        <ItemCreator :level="this.level" />
      </div>

      <!-- Zone de contrôle et d'output -->
      <div id="interface">
        <div id="controls">
          <h2 id="niveau">Niveau {{ this.level }}</h2>
          <h3 id="instruction">{{ this.interface[this.level - 1].instructionSubtitle }}</h3>
          <p id="aide">
            Utilisez
            <span class="dom-code" @click="addCodeToCommandInput">
              {{ this.interface[this.level - 1].helpParagraphe[0] }}
            </span>
            {{ this.interface[this.level - 1].helpParagraphe[1] }}
          </p>
          <label for="commande">
            const bateau =
            <input type="text" id="commande" v-model="commande" placeholder="Entrez votre commande JS ici">
          </label>
          <button id="valider" @click="checkResponse()">Valider</button>
        </div>
        <div id="output">
          <h2> {{ this.output }} </h2>
          <p v-html="this.lesson"></p>
          
          <button v-if="showNextButton" @click="nextLevel">Niveau Suivant</button>
        </div>
      
       

      </div>
    </div>
  </div>
</template>

<script>
import ItemCreator from './components/ItemCreator.vue';


export default {
  name: 'App',
  components: {
    ItemCreator,
  },

  data() {
    return {
      level: 1,
      output: "",
      lesson: "",
      showNextButton: false,
      commande: null,
      interface: [
        {
          id: 1,
          instructionSubtitle: 'Sélectionner un élément avec son id',
          helpParagraphe: ["document.getElementById('id_de_l\'élément')", "pour trouver le bateau !"],
          goodAnswers: ["document.getElementById('bateau1')","document.getElementById('bateau1');","document.getElementById(\"bateau1\")","document.getElementById(\"bateau1\");"],
          lesson: "La méthode getElementById() de l'interface Document renvoie un objet Element représentant l'élément dont la propriété id correspond à la chaîne de caractères spécifiée. Étant donné que les ID d'élément doivent être uniques, s'ils sont spécifiés, ils constituent un moyen utile d'accéder rapidement à un élément spécifique. pour plus d'information : <a href='https://developer.mozilla.org/fr/docs/Web/API/Document/getElementById'>https://developer.mozilla.org/fr/docs/Web/API/Document/getElementById</a>"
        },
        {
          id: 2,
          instructionSubtitle: 'Sélectionner plusieurs éléments avec leur classe',
          helpParagraphe: ["document.getElementsByClassName('nom_de_la_classe')", "pour sélectionner tous les bateaux avec la même classe !"],
          goodAnswer: "document.getElementsByClassName('bateaux')"
        },
        {
          id: 3,
          instructionSubtitle: 'Sélectionner le premier bateau avec querySelector',
          helpParagraphe: ["document.querySelector('.nom_de_la_classe')", "pour trouver le premier bateau d'une classe !"],
          goodAnswer: "document.querySelector('.bateau')"
        },
      ],
    }
  },
  methods: {
    checkResponse() {


      if (this.interface[this.level - 1].goodAnswers.find(answers => answers === this.commande)) {
        this.output = this.commande + " est la bonne réponse ";
        this.lesson = this.interface[this.level - 1].lesson
        this.showNextButton = true;
      } else {
        this.output = "vous avez commis une erreur";
      }

    },
    nextLevel() {
      if (this.level < this.interface.length) {
        this.level++;
        this.output = ""; // Réinitialiser l'output
        this.lesson = "";
        this.commande = ""; // Réinitialiser la commande
        this.showNextButton = false; // Cacher le bouton pour le nouveau niveau
      }
    },
    addCodeToCommandInput() {
      this.commande = this.interface[this.level - 1].helpParagraphe[0];
    },
  },
}
</script>

<style scoped>
/* Style général */
#game-body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  background-color: #87ceeb;
  /* Ciel */
}

/* Conteneur principal */
#container {
  display: flex;
  width: 90%;
  height: 70%;
  border: 2px solid #333;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
}

/* Zone de la mer */
#map {
  flex: 2;
  background-color: #1e90ff;
  /* Mer */
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

/* Interface utilisateur */
#interface {
  flex: 1;
  background-color: #f0f0f0;
  display: flex;
  flex-direction: column;
  padding: 20px;
  box-sizing: border-box;
  border-left: 2px solid #333;
}

#controls {
  margin-bottom: 20px;
}

#controls label {
  display: block;
  margin: 10px 0;
  font-size: 16px;
}

#commande {
  padding: 5px;
  width: 65%;
  font-size: 16px;
}

#valider {
  padding: 5px 10px;
  font-size: 16px;
  cursor: pointer;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
}

#valider:hover {
  background-color: #0056b3;
}

#output {
  font-size: 16px;
  color: #333;
  background-color: #fff;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

.dom-code {
  font-weight: bold;
}

.dom-code:hover {
  background-color: rgba(0, 100, 126, 0.6);
  color: white;
}


</style>
