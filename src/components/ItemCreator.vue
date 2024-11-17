<template>

  <div v-for="(ship, index) in this.levels[this.level - 1].ships" :key="index" :id="ship.id" :class="ship.class">
    <img :src="this.pirateShipImage" alt="Pirate Ship" class="ship" />
    <div class="tooltip">
      id="{{ ship.id }}" class="{{ ship.class }}"
    </div>
  </div>


</template>

<script>
export default {
  props: ["level"],

  data() {
    return {
      levelTest: 2,
      levels: [
        {
          level: 1,
          ships: [
            {
              id: 'bateau1',
              class: 'bateau'
            }
          ]
        },
        {
          level: 2,
          ships: [
            {
              id: 'bateau1',
              class: 'bateaux'
            },
            {
              id: 'bateau2',
              class: 'bateaux'
            },
            {
              id: 'bateau3',
              class: 'bateaux'
            }
          ]
        },
        {
          level: 3,
          ships: [
            {
              id: 'bateau1',
              class: 'bateaux'
            },
            {
              id: 'bateau2',
              class: 'bateaux'
            },
            {
              id: 'bateau3',
              class: 'bateaux'
            }
          ]
        },

      ]

    }
  },

  computed: {
    pirateShipImage() {
      return new URL('@/assets/images/pirate-ship.png', import.meta.url).href;
    },
  },
}
</script>

<style>
/* Le bateau */
.bateau,
.bateaux {
  width: 250px;
  color: white;
  line-height: 50px;
  border: 2px solid black;
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
.ship {
  width: 100%;
}

/* Effet au survol */
.bateau:hover,
.bateaux:hover{
  transform: scale(1.1);
  box-shadow: 0px 0px 10px 10px #09fa00;
}

/* Étiquette pour les bateaux */
.tooltip {
  position: absolute;
  background-color: rgba(0, 0, 0);
  color: white;
  padding: 5px 10px;
  border-radius: 5px;
  font-size: 14px;
  pointer-events: none;
  display: none;
  z-index: 1000;
  top: -20px;
}

.bateau:hover .tooltip,
.bateaux:hover .tooltip {
  display: block;
}

.bateau.cible,
.bateaux.cible {
  background-color: red;
  color: yellow;
}
</style>
