<template>
  <div id="game-body">
    <div id="container">
      <!-- Zone de jeu -->
      <div id="map">
        <ItemCreator :level="level" />
      </div>

      <!-- Interface utilisateur -->
      <div id="interface">
        <div id="controls">
          <h2 id="niveau">Niveau {{ level }}</h2>
          <h3 id="instruction">{{ currentLevel().subtitle }}</h3>
          <p id="aide">
            Créez une variable <span>"{{ currentLevel().variable }}"</span> qui a pour valeur :
            <span class="dom-code" @click="addCodeToCommandInput">
              {{ currentLevel().help.code }}
            </span>
            {{ currentLevel().help.description }}
          </p>
          <label for="commande">
            <div>
              <textarea id="commande" v-model="commande" placeholder="Entrez votre commande JS ici"></textarea>
            </div>
          </label>
          <button id="valider" @click="checkResponse">Valider</button>
        </div>
        <div id="output">
          <h2 v-html="output" id="output-title"></h2>
          <p v-html="lesson"></p>
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
      commande: "", // Texte saisi par l'utilisateur
      interface: [
        {
          id: 1,
          instructionSubtitle: 'Sélectionner un élément avec son id',
          help: {
            code: "document.getElementById('id_de_l\'élément')",
            description: "pour sélectionner le bateau !",
          },
          variable: "bateau",

          answerPattern: /^(const|let|var)\s+[a-zA-Z_$][a-zA-Z_$0-9]*\s*=\s*document\.getElementById\(["'][a-zA-Z0-9_-]+["']\);?$/
          ,
          lesson: "La méthode getElementById() de l'interface Document renvoie un objet Element représentant l'élément dont la propriété id correspond à la chaîne de caractères spécifiée. Étant donné que les ID d'élément doivent être uniques, s'ils sont spécifiés, ils constituent un moyen utile d'accéder rapidement à un élément spécifique. pour plus d'information : <a href='https://developer.mozilla.org/fr/docs/Web/API/Document/getElementById'>https://developer.mozilla.org/fr/docs/Web/API/Document/getElementById</a>"
        },
        {
          id: 2,
          instructionSubtitle: 'Sélectionner plusieurs éléments avec leur classe',
          help: {
            code: "document.getElementsByClassName('nom_de_la_classe')",
            description: "pour sélectionner tous les bateaux avec la même classe !",
          },
          variable: "bateaux",
          answerPattern: /^(const|let|var)\s+[a-zA-Z_$][a-zA-Z_$0-9]*\s*=\s*document\.getElementsByClassName\(["']bateaux["']\);?$/,
          lesson: "Renvoie un objet de type tableau de tous les éléments enfants qui ont tous les noms de classe donnés. Lorsqu'il est appelé sur l'objet document, le document complet est recherché, y compris le nœud racine. Vous pouvez également appeler getElementsByClassName () sur n'importe quel élément; il retournera uniquement les éléments qui sont les descendants de l'élément racine spécifié avec les noms de classes donnés. Pour plus d'information : <a href='https://developer.mozilla.org/fr/docs/Web/API/Document/getElementsByClassName'>https://developer.mozilla.org/fr/docs/Web/API/Document/getElementsByClassName</a>"
        },
        {
          id: 3,
          instructionSubtitle: 'Sélectionner le premier bateau avec querySelector',
          help: {
            code: "document.querySelector('.nom_de_la_classe')",
            description: "pour sélectionner uniquement le premier bateau d'une classe !"
          },
          variable: "bateau1",
          answerPattern: /^(const|let|var)\s+[a-zA-Z_$][a-zA-Z_$0-9]*\s*=\s*document\.querySelector\(["']\.bateaux["']\);?$/,
          lesson: "La méthode querySelector() de l'interface Document retourne le premier Element dans le document correspondant au sélecteur - ou groupe de sélecteurs - spécifié(s), ou null si aucune correspondance n'est trouvée. Pour plus d'information : <a href='https://developer.mozilla.org/fr/docs/Web/API/Document/querySelector'>https://developer.mozilla.org/fr/docs/Web/API/Document/querySelector</a>"
        },
      ],
    };
  },
  methods: {
    currentLevel() {
      return this.interface[this.level - 1];
    },
    checkResponse() {
      const current = this.currentLevel();
      const userCommand = this.commande.trim();

      if (current.answerPattern.test(userCommand)) {
        this.output = `${userCommand} <br/> est la bonne réponse.`
        this.lesson = current.lesson;
        this.showNextButton = true;
      } else {
        this.output = "Vous avez commis une erreur.";
      }
    },
    nextLevel() {
      if (this.level < this.interface.length) {
        this.level++;
        this.resetLevelState();
      }
    },
    resetLevelState() {
      this.output = ""; // Réinitialiser l'output
      this.lesson = "";
      this.commande = ""; // Réinitialiser la commande
      this.showNextButton = false; // Cacher le bouton pour le nouveau niveau
    },
    addCodeToCommandInput() {
      this.commande = "const " + this.currentLevel().variable + " = " + this.currentLevel().help.code;
    },
  },
};
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
  width: 95%;
  height: 80%;
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

#controls textarea {
  display: block;
  margin: 10px 0;
  width: 100%;
  font-size: 16px;
}

#commande {
  padding: 5px;
  width: 65%;
  font-size: 16px;
  resize: none;
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

#output-title {
  font-size: 20px;
  font-style: italic;
  margin-bottom: 25px;
}

#aide span {
  font-weight: bold;
}

.dom-code:hover {
  background-color: rgba(0, 100, 126, 0.6);
  color: white;
}

</style>
