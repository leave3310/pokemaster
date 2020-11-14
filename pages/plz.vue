<template>
  <v-container>
    <v-row justify="center">
      <v-col cols="12" md="6">
        <v-subheader>屬性</v-subheader>
        <v-select
          v-model="chosAPI.chosAttr"
          :items="attributes"
          item-text="state"
          item-value="api"
          prepend-icon="mdi-map"
          :menu-props="{ maxHeight: '400' }"
        ></v-select>
        <v-subheader class="text--center">地區</v-subheader>
        <v-select
          v-model="chosAPI.chosReg"
          :items="regions"
          item-text="state"
          item-value="api"
          prepend-icon="mdi-map"
          :menu-props="{ maxHeight: '400' }"
        ></v-select>
        <v-btn @click="search">
          <v-icon>mdi-magnify</v-icon>
          搜尋
        </v-btn>
      </v-col>

      <v-col cols="12" md="6" class="d-flex align-center">
        <v-sheet elevation="3" class="pa-4">
          <v-chip-group v-model="chosPoke" column active-class="primary--text">
            <v-chip v-for="tag in chosseablePoke" :key="tag">
              {{ tag }}
            </v-chip>
          </v-chip-group>
          <v-btn @click="search1">go</v-btn>
        </v-sheet>
      </v-col>
      <v-col col="6" offset-md="4">
        <v-card max-width="400">
          <v-img width="100px" :src="pic"></v-img>
          <v-card-title v-if="test">{{ res.species.name }}</v-card-title>
          <v-card-text v-if="test">id:{{ res.id }}</v-card-text>
          <v-card-text v-if="test">
            type:
            <span v-for="(item, i) in res.types" :key="i">
              {{ item.type.name }}
            </span>
          </v-card-text>
          <v-card-text v-if="test">
            weight:
            <span>{{ res.weight / 10 }}kg</span>
          </v-card-text>
          <v-card-text v-if="test">
            height:
            <span>{{ res.height / 10 }}m</span>
          </v-card-text>
          <v-card-text v-if="test">
            hp:
            <span>{{ res.stats[0]['base_stat'] }}</span>
          </v-card-text>
          <v-card-text v-if="test">
            attack:
            <span>{{ res.stats[1]['base_stat'] }}</span>
          </v-card-text>
          <v-card-text v-if="test">
            defense:
            <span>{{ res.stats[2]['base_stat'] }}</span>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      pic: '',
      test: false,
      res: null,
      attributes: [
        { state: '一般', api: 1 },
        { state: '火', api: 10 },
        { state: '水', api: 11 },
        { state: '草', api: 12 },
        { state: '電', api: 13 },
        { state: '冰', api: 15 },
        { state: '格鬥', api: 2 },
        { state: '飛行', api: 3 },
        { state: '毒', api: 4 },
        { state: '地面', api: 5 },
        { state: '岩石', api: 6 },
        { state: '蟲', api: 7 },
        { state: '幽靈', api: 8 },
        { state: '鋼', api: 9 },
        { state: '超能力', api: 14 },
        { state: '龍', api: 16 },
        { state: '惡', api: 17 },
        { state: '妖精', api: 18 },
      ],
      regions: [
        { state: '關都', api: 2 },
        { state: '成都', api: 7 },
        { state: '豐原', api: 15 },
        { state: '神奧', api: 6 },
        { state: '合眾', api: 9 },
      ],
      chosAPI: { chosAttr: 18, chosReg: 9 },
      chosseablePoke: [],
      chosPoke: 'Pokemon',
    }
  },
  methods: {
    async search() {
      let res1 = await this.$axios.$get(
        `https://pokeapi.co/api/v2/type/${this.chosAPI.chosAttr}/`
      )
      res1 = res1.pokemon
      let res2 = await this.$axios.$get(
        `https://pokeapi.co/api/v2/pokedex/${this.chosAPI.chosReg}/`
      )
      res2 = res2.pokemon_entries
      const ansAry = []
      for (let i = 0; i < res1.length; i++) {
        for (let t = 0; t < res2.length; t++) {
          if (res2[t].pokemon_species.name === res1[i].pokemon.name) {
            ansAry.push(res1[i].pokemon.name)
          }
        }
      }
      this.chosseablePoke = [...ansAry]
    },
    async search1() {
      this.res = await this.$axios.$get(
        `https://pokeapi.co/api/v2/pokemon/${
          this.chosseablePoke[this.chosPoke]
        }`
      )
      this.pic = `https://pokeres.bastionbot.org/images/pokemon/${this.res.id}.png`
      this.test = true
    },
  },
}
</script>

<style></style>
