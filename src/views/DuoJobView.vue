<script>
import { RouterLink } from 'vue-router'
export default {
  data() {
    return {
      currentElo: [
        {
          name: 'Ferro',
          leagues: [{ name: 'I' }, { name: 'II' }, { name: 'III' }, { name: 'IV' }],
          visible: true,
          type: 'current',
          image: '/src/assets/iron.png'
        },
        {
          name: 'Bronze',
          leagues: [{ name: 'I' }, { name: 'II' }, { name: 'III' }, { name: 'IV' }],
          visible: true,
          type: 'current',
          image: '/src/assets/bronze.png'
        },
        {
          name: 'Prata',
          leagues: [{ name: 'I' }, { name: 'II' }, { name: 'III' }, { name: 'IV' }],
          visible: true,
          type: 'current',
          image: '/src/assets/silver.png'
        },
        {
          name: 'Ouro',
          leagues: [{ name: 'I' }, { name: 'II' }, { name: 'III' }, { name: 'IV' }],
          visible: true,
          type: 'current',
          image: '/src/assets/gold.png'
        },
        {
          name: 'Platina',
          leagues: [{ name: 'I' }, { name: 'II' }, { name: 'III' }, { name: 'IV' }],
          visible: true,
          type: 'current',
          image: '/src/assets/platinum.png'
        },
        {
          name: 'Esmeralda',
          leagues: [{ name: 'I' }, { name: 'II' }, { name: 'III' }, { name: 'IV' }],
          visible: true,
          type: 'current',
          image: '/src/assets/emerald.png'
        },
        {
          name: 'Diamante',
          leagues: [{ name: 'I' }, { name: 'II' }, { name: 'III' }, { name: 'IV' }],
          visible: true,
          type: 'current',
          image: '/src/assets/diamond.png'
        },
        {
          name: 'Mestre - Flex',
          leagues: null,
          visible: true,
          type: 'current',
          image: '/src/assets/master.png'
        },
        {
          name: 'Grão Mestre - Flex',
          leagues: null,
          visible: true,
          type: 'current',
          image: '/src/assets/grandmaster.png'
        }
      ],

      targetElo: [
        {
          name: 'Ferro',
          leagues: [{ name: 'I' }, { name: 'II' }, { name: 'III' }, { name: 'IV' }],
          visible: true,
          type: 'target',
          image: '/src/assets/iron.png'
        },
        {
          name: 'Bronze',
          leagues: [{ name: 'I' }, { name: 'II' }, { name: 'III' }, { name: 'IV' }],
          visible: true,
          type: 'target',
          image: '/src/assets/bronze.png'
        },
        {
          name: 'Prata',
          leagues: [{ name: 'I' }, { name: 'II' }, { name: 'III' }, { name: 'IV' }],
          visible: true,
          type: 'target',
          image: '/src/assets/silver.png'
        },
        {
          name: 'Ouro',
          leagues: [{ name: 'I' }, { name: 'II' }, { name: 'III' }, { name: 'IV' }],
          visible: true,
          type: 'target',
          image: '/src/assets/gold.png'
        },
        {
          name: 'Platina',
          leagues: [{ name: 'I' }, { name: 'II' }, { name: 'III' }, { name: 'IV' }],
          visible: true,
          type: 'target',
          image: '/src/assets/platinum.png'
        },
        {
          name: 'Esmeralda',
          leagues: [{ name: 'I' }, { name: 'II' }, { name: 'III' }, { name: 'IV' }],
          visible: true,
          type: 'target',
          image: '/src/assets/emerald.png'
        },
        {
          name: 'Diamante',
          leagues: [{ name: 'I' }, { name: 'II' }, { name: 'III' }, { name: 'IV' }],
          visible: true,
          type: 'target',
          image: '/src/assets/diamond.png'
        },
        {
          name: 'Mestre',
          leagues: null,
          visible: true,
          type: 'target',
          image: '/src/assets/master.png'
        },
        {
          name: 'Grão Mestre - Flex',
          leagues: null,
          visible: true,
          type: 'target',
          image: '/src/assets/grandmaster.png'
        },
        {
          name: 'Desafiante - Flex',
          leagues: null,
          visible: true,
          type: 'target',
          image: '/src/assets/challenger.png'
        }
      ],

      priceList: [
        { name: 'Ferro', value: 15 },
        { name: 'Bronze', value: 15 },
        { name: 'Prata', value: 17.5 },
        { name: 'Ouro', value: 20 },
        { name: 'Platina', value: 30 },
        { name: 'Esmeralda', value: 45 },
        { name: 'Diamante', value: 65 },
        { name: 'Mestre', value: 600 },
        { name: 'Grão Mestre', value: 1200 },
        { name: 'Desafiante', value: 0 }
      ],

      selectedElo: {
        current: { name: null, league: null, index: null, image: null },
        target: { name: null, league: null, index: null, image: null }
      },

      computedEloArray: [],
      totalPrice: null,
      totalLeagues: null
    }
  },
  methods: {
    toggleSelectorCurrent(elo, index) {
      // Calcular preço do elojob
      if (this.selectedElo.current.name != null && this.selectedElo.target.name != null) {
        this.getComputedElo()
      }

      // Ao selecionar diamante-, mostrar seletor de divisão ao clicar
      if (index <= 6) {
        this.currentElo.forEach((elo, i) => {
          if (i === index) {
            elo.visible = !elo.visible
          } else {
            elo.visible = true
          }
        })
      } else {
        this.currentElo.forEach((elo) => {
          elo.visible = true
        })
      }

      // Fechar seletor de divisão da coluna oposta (estética)
      this.targetElo.forEach((elo) => {
        elo.visible = true
      })
    },

    toggleSelectorTarget(elo, index) {
      // Calcular preço do elojob
      if (this.selectedElo.current.name != null && this.selectedElo.target.name != null) {
        this.getComputedElo()
      }

      // Ao selecionar diamante-, mostrar seletor de divisão ao clicar
      if (index <= 6) {
        this.targetElo.forEach((elo, i) => {
          if (i === index) {
            elo.visible = !elo.visible
          } else {
            elo.visible = true
          }
        })
      } else {
        this.targetElo.forEach((elo) => {
          elo.visible = true
        })
      }

      // Fechar seletor de divisão da coluna oposta (estética)
      this.currentElo.forEach((elo) => {
        elo.visible = true
      })
    },

    selectElo(elo, index, leagueIndex) {
      if (elo.type == 'current') {
        // Entre ferro e diamante, (executado apenas ao clicar na divisão, não no elo)
        if (index <= 6 && leagueIndex != null) {
          // Reseta selectedElo caso seja inferior elo atual
          if (
            index > this.selectedElo.target.index ||
            (index == this.selectedElo.target.index &&
              leagueIndex <= this.selectedElo.target.league)
          ) {
            this.resetSelection()
          }

          this.selectedElo.current.name = elo.name
          this.selectedElo.current.image = elo.image
          this.selectedElo.current.league = leagueIndex
          this.selectedElo.current.index = index
        }

        // Entre mestre e desafiante
        if (index >= 7) {
          if (index >= this.selectedElo.target.index) {
            this.resetSelection()
          }

          this.selectedElo.current.name = elo.name
          this.selectedElo.current.image = elo.image
          this.selectedElo.current.league = 0
          this.selectedElo.current.index = index
        }

        this.toggleSelectorCurrent(elo, index)
      }

      if (elo.type == 'target') {
        // Bloquear seleção caso o elo seja: inferior ao elo atual EX: (Platina ao Ouro) ou mesmo elo porém com divisão inferior EX: (Platina 2 ao Platina 4)
        if (
          index < this.selectedElo.current.index ||
          (index == this.selectedElo.current.index &&
            leagueIndex >= this.selectedElo.current.league)
        ) {
          return
        }

        // Entre ferro e diamante, (executado apenas ao clicar na divisão, não no elo)
        if (index <= 6 && leagueIndex != null) {
          this.selectedElo.target.name = elo.name
          this.selectedElo.target.image = elo.image
          this.selectedElo.target.league = leagueIndex
          this.selectedElo.target.index = index
        }

        // Entre mestre e desafiante
        if (index >= 7) {
          // Bloquear seleção caso o elo seja igual ao elo atual (Ex: Mestre - Mestre)
          if (index == this.selectedElo.current.index) {
            return
          }

          this.selectedElo.target.name = elo.name
          this.selectedElo.target.image = elo.image
          this.selectedElo.target.league = 0
          this.selectedElo.target.index = index
        }
        this.toggleSelectorTarget(elo, index)
      }
    },

    resetSelection() {
      this.selectedElo.target.name = null
      this.selectedElo.target.league = null
      this.selectedElo.target.index = null
      this.computedEloArray = []
      this.totalPrice = 0
      this.totalLeagues = 0
    },

    getComputedElo() {
      const currentIndex = this.selectedElo.current.index
      const targetIndex = this.selectedElo.target.index

      this.computedEloArray = [] // Limpa o array antes de calcular novamente
      this.totalPrice = 0
      this.totalLeagues = 0

      for (let index = currentIndex; index <= targetIndex; index++) {
        const currentElo = { ...this.currentElo[index] }
        const price = this.priceList[index]
        let multiplier = 4

        // Elos acima do mestre recebem multiplier = 1
        if (index >= 7) {
          multiplier = 1
        }

        // O elo inicial selecionado recebe o multiplicador conforme a liga selecionada / First run
        if (index == currentIndex && index <= 6) {
          multiplier = this.selectedElo.current.league + 1
        }

        // O elo final selecionado recebe o multiplicador inverso a liga selecionada / Last run
        if (index == targetIndex) {
          if (index <= 6) {
            switch (this.selectedElo.target.league) {
              case 3:
                multiplier = 0
                return
              case 2:
                multiplier = 1
                break
              case 1:
                multiplier = 2
                break
              case 0:
                multiplier = 3
                break
            }
          } else {
            return
          }
        }

        // Caso o elo final seja igual ao elo inicial, calcular preço por divisão:
        if (currentIndex == targetIndex) {
          multiplier = this.selectedElo.current.league - this.selectedElo.target.league
        }

        const computedElo = {
          name: currentElo.name,
          price: price.value,
          index: index,
          multiplier: multiplier
        }

        // Calcular quantidade de ligas, para calcular prazoo
        if (index <= 6) {
          this.totalLeagues += multiplier
        } else {
          this.totalLeagues += 7
        }

        this.computedEloArray.push(computedElo)
        this.totalPrice += computedElo.price * computedElo.multiplier
      }
    }
  }
}
</script>
<template>
  <main id="main">
    <div :class="{ content: !totalPrice, contentTrue: totalPrice }">
      <div class="rankBox">
        <div class="rank-column">
          <div class="rank-row">
            <span class="row-title">Elo inicial</span>
          </div>
          <template v-for="(elo, index) in currentElo" :key="index">
            <div class="rank-row">
              <span
                class="row-elo"
                @click="selectElo(elo, index)"
                v-if="elo.visible"
                :class="{ 'row-elo-selected': elo.name == selectedElo.current.name }"
              >
                {{ elo.name }}
                <img :src="elo.image" />
              </span>
              <div class="row-league" v-if="!elo.visible">
                <template v-for="(league, leagueIndex) in elo.leagues" :key="leagueIndex">
                  <span class="league-item" @click="selectElo(elo, index, leagueIndex)">
                    {{ league.name }}
                  </span>
                </template>
              </div>
            </div>
          </template>
        </div>

        <div class="rank-column">
          <div class="rank-row">
            <span class="row-title">Elo final</span>
          </div>
          <template v-for="(elo, index) in targetElo" :key="index">
            <div
              class="rank-row"
              v-if="
                index >= selectedElo.current.index &&
                !(index == selectedElo.current.index && selectedElo.current.league == 0)
              "
            >
              <span
                class="row-elo"
                @click="selectElo(elo, index)"
                v-if="elo.visible"
                :class="{
                  'row-elo-selected': elo.name == selectedElo.target.name,
                  blockSelection:
                    index < selectedElo.current.index ||
                    (index >= 7 && index == selectedElo.current.index)
                }"
              >
                {{ elo.name }}
                <img :src="elo.image" />
              </span>
              <div class="row-league" v-if="!elo.visible">
                <template v-for="(league, leagueIndex) in elo.leagues" :key="leagueIndex">
                  <span
                    class="league-item"
                    @click="selectElo(elo, index, leagueIndex)"
                    :class="{
                      blockSelection:
                        index == selectedElo.current.index &&
                        leagueIndex >= selectedElo.current.league
                    }"
                  >
                    {{ league.name }}
                  </span>
                </template>
              </div>
            </div>
          </template>
        </div>
      </div>

      <div id="priceBox" v-if="totalPrice">
        <body class="priceBox-body">
          <div class="priceBox-body-block">
            <img :src="selectedElo.current.image" alt="" />
            <p>{{ selectedElo.current.name }} {{ selectedElo.current.league + 1 }}</p>
          </div>
          <div class="priceBox-body-block">Ao</div>
          <div class="priceBox-body-block">
            <img :src="selectedElo.target.image" alt="" />
            <p>{{ selectedElo.target.name }} {{ selectedElo.target.league + 1 }}</p>
          </div>
        </body>
        <footer class="priceBox-footer">
          <div class="priceBox-footer">
            <RouterLink
              class="priceBox-footer-value"
              :to="{
                path: '/payment',
                query: {
                  totalPrice: totalPrice,
                  currentEloName: selectedElo.current.name + ' ' + (selectedElo.current.league + 1),
                  currentEloImage: selectedElo.current.image,
                  targetEloName: selectedElo.target.name + ' ' + (selectedElo.target.league + 1),
                  targetEloImage: selectedElo.target.image,
                  deadline: totalLeagues * 2
                }
              }"
              >Confirmar R${{ totalPrice }}</RouterLink
            >
          </div>
        </footer>
      </div>
    </div>
  </main>
</template>

<style scoped>
#main {
  background-color: rgba(0, 0, 0, 0.8);

  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 1fr;
  padding: 40px;
}

.content {
  display: grid;
  grid-template-columns: 1fr;
  justify-items: center;
}

.contentTrue {
  margin: 40px;

  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 5px;
}

.rankBox {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  row-gap: 20px;
  width: 40vw;
  gap: 5px;
}

.rank-column {
  display: grid;
  grid-template-rows: repeat(11, 1fr);
}

.rank-row {
  display: flex;
  cursor: pointer;
}

.row-title {
  flex-grow: 1;

  display: flex;
  justify-content: center;
  align-items: center;

  font-weight: bold;
  font-size: 1.5rem;
  text-align: center;
  padding-inline: 5px;
}

.row-elo {
  flex-grow: 1;

  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  gap: 5px;
}
.row-elo > img {
  height: 1.5rem;
}

.row-elo:hover {
  background-color: var(--selectHover);
}

.row-elo-selected {
  background-color: var(--selectTrue);
}

.row-elo-selected:hover {
  background-color: var(--selectTrue);
}

.row-league {
  flex: 1;

  display: grid;
  grid-template-columns: repeat(4, 1fr);
}

.league-item {
  display: flex;
  justify-content: center;
  align-items: center;
}

.league-item:hover {
  background-color: var(--selectHover);
}

.blockSelection:hover {
  background-color: var(--blockSelection);
}
.blockSelection:active {
  animation: shake 0.2s alternate;
}

@keyframes shake {
  0% {
    transform: translateX(0);
  }
  50% {
    transform: translateX(-5px);
  }
  100% {
    transform: translateX(5px);
  }
}

#priceBox {
  display: grid;
  grid-template-rows: 6fr 1fr;
  align-self: center;

  align-items: center;
  height: fit-content;
}

.priceBox-body {
  display: flex;
  justify-content: space-evenly;
}

.priceBox-body-block {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  gap: 20px;
}

.priceBox-body-block > img {
  height: 4rem;
}

.priceBox-footer {
  display: flex;
  justify-content: center;
  align-items: center;
}
.priceBox-footer-value {
  cursor: pointer;
  font-size: 1.5rem;
  background-color: rgb(16, 184, 121);
  color: black;

  border-radius: 10px;
  padding: 7px;
  border: 5px double black;
}
.priceBox-footer-value:hover {
  background-color: rgb(16, 144, 121);
}
</style>