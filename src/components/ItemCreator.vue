<template>
  <div v-for="(item, index) in this.levels[this.level - 1].items" :key="index" :id="item.id" :class="item.class">
    <img :src="item.image" alt="item image" class="item" />
    <div class="tooltip">
      id="{{ item.id }}" class="{{ item.class }}"
    </div>
  </div>
</template>



<script>
export default {
  props: ["level"],

  data() {
    return {
      levels: [
        {
          level: 1,
          items: [
            { id: "bateau1", class: "bateaux", image: this.getImageUrl('../assets/images/pirate-ship.png') },
          ],
        },
        {
          level: 2,
          items: [
            { id: "bateau1", class: "bateaux", image: this.getImageUrl('../assets/images/pirate-ship.png') },
            { id: "bateau2", class: "bateaux", image: this.getImageUrl('../assets/images/pirate-ship.png') },
            { id: "bateau3", class: "bateaux", image: this.getImageUrl('../assets/images/pirate-ship.png') },
          ],
        },
        {
          level: 3,
          items: [
            { id: "bateau1", class: "bateaux", image: this.getImageUrl('../assets/images/pirate-ship.png') },
            { id: "tresor", class: "tresors", image: this.getImageUrl('../assets/images/tresor-pirate.png') },
            { id: "bateau2", class: "bateaux", image: this.getImageUrl('../assets/images/pirate-ship.png') },
          ],
        },
        {
          level: 4,
          items: [
            { id: "bateau1", class: "bateaux", image: this.getImageUrl('@/assets/images/pirate-ship.png') },
            { id: "bateau2", class: "bateaux", image: this.getImageUrl('@/assets/images/pirate-ship.png') },
            { id: "bateau3", class: "bateaux", image: this.getImageUrl('@/assets/images/pirate-ship.png') },
          ],
        },
      ],
    };
  },

  methods: {
    getImageUrl(imagePath) {
      return new URL(imagePath, import.meta.url).href;
    },
  },
};
</script>


<style>
/* Le bateau */
.bateau,
.bateaux {
  width: 250px;
  color: white;
  line-height: 50px;
  border-radius: 5px;
  transition: all 0.3s ease-in-out;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  position: relative;
  margin-right: 20px;
}

/* Image de bateau pirate */
.item {
  width: 100%;
}

/* Étiquette pour les bateaux */
.tooltip {
  position: absolute;
  background-color: rgba(0, 0, 0, 0.7);
  color: white;
  padding: 5px 10px;
  border-radius: 5px;
  font-size: 14px;
  pointer-events: none;
  display: none;
  z-index: 1000;
  top: -20px;
}

/* Effet au survol de l'élément pour faire apparaitre les informations*/
.bateaux:hover .tooltip {
  display: block;
}

/* Effet au survol de l'élément */
.bateaux:hover img {
  transform: scale(1.2);
  filter: brightness(1.25);
}

/* Effet sur les éléments non survolés */
.bateaux:not(:hover) img {
  filter: brightness(0.7);
}
</style>
