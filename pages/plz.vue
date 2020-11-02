<template>
  <v-container fill-height>
    <v-row>
      <v-col cols="6">
        <v-menu offset-y>
          <template v-slot:activator="{ on, attrs }">
            <v-btn color="primary" dark v-bind="attrs" v-on="on">
              {{ attributes[chosAttr] }}
            </v-btn>
          </template>
          <v-list>
            <v-list-item-group v-model="chosAttr">
              <v-list-item v-for="(item, i) in attributes" :key="i">
                <v-list-item-content>
                  <v-list-item-title>{{ item }}</v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-menu>
        <v-menu offset-y>
          <template v-slot:activator="{ on, attrs }">
            <v-btn color="primary" dark v-bind="attrs" v-on="on">
              {{ regions[chosReg] }}
            </v-btn>
          </template>
          <v-list>
            <v-list-item-group v-model="chosReg">
              <v-list-item v-for="(item, i) in regions" :key="i">
                <v-list-item-content>
                  <v-list-item-title>{{ item }}</v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-menu>
        <v-btn @click="search">
          <v-icon>mdi-magnify</v-icon>
        </v-btn>
        <v-menu offset-y>
          <template v-slot:activator="{ on, attrs }">
            <v-btn color="primary" dark v-bind="attrs" v-on="on">
              {{ chosseablePoke[chosPoke] }}
            </v-btn>
          </template>
          <v-list>
            <v-list-item-group v-model="chosPoke">
              <v-list-item v-for="(item, i) in chosseablePoke" :key="i">
                <v-list-item-content>
                  <v-list-item-title>{{ item }}</v-list-item-title>
                </v-list-item-content>
              </v-list-item>
            </v-list-item-group>
          </v-list>
        </v-menu>
        <v-btn @click="search1">go</v-btn>
      </v-col>
      <v-col col="6">
        <v-card>
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
        '一般',
        '火',
        '水',
        '草',
        '電',
        '冰',
        '格鬥',
        '飛行',
        '毒',
        '地面',
        '岩石',
        '蟲',
        '幽靈',
        '鋼',
        '超能力',
        '龍',
        '惡',
        '妖精',
      ],
      attributesApi: [
        1,
        10,
        11,
        12,
        13,
        15,
        2,
        3,
        4,
        5,
        6,
        7,
        8,
        9,
        14,
        16,
        17,
        18,
      ],
      regions: ['關都', '成都', '豐原', '神奧', '合眾'],
      regionsApi: [2, 7, 15, 6, 9],
      chosAttr: 'attribute',
      chosReg: 'region',
      chosseablePoke: [],
      chosPoke: 'Pokemon',
    }
  },
  methods: {
    async search() {
      let res1 = await this.$axios.$get(
        `https://pokeapi.co/api/v2/type/${this.attributesApi[this.chosAttr]}/`
      )
      res1 = res1.pokemon
      let res2 = await this.$axios.$get(
        `https://pokeapi.co/api/v2/pokedex/${this.regionsApi[this.chosReg]}/`
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
