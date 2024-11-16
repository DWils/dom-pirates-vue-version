<template>
  <div id="game-body">
    <div id="container">
      <!-- Zone de jeu : la mer -->
      <div id="map">
        <ItemCreator :level="this.level"/>
      </div>

      <!-- Zone de contrôle et d'output -->
      <div id="interface">
        <div id="controls">
          <h2 id="niveau">Niveau 1</h2>
          <h3 id="instruction">Sélectionner un élément avec son id</h3>
          <p id="aide">
            Utilisez <span>document.getElementById('id_de_l'élément')</span> pour trouver le bateau !
          </p>
          <label for="commande">
            const bateau =
            <input type="text" id="commande" placeholder="Entrez votre commande JS ici">
          </label>
          <button id="valider">Valider</button>
        </div>
        <div id="output"></div>
      </div>
    </div>
  </div>
</template>

<script>
import ItemCreator from './components/ItemCreator.vue';

export default {
  name: 'App',
  components: {
    ItemCreator
  },

  data(){
    return {
      level: 1,
    }
  }
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

#aide span{
  font-weight: bold;
}

#aide span:hover {
    background-color: rgba(0, 107, 126, 0.2);
  }
</style>
