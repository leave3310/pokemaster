<template>
  <v-container fill-height>
    <v-row>
      <v-col cols="12">
        <v-text-field v-model="pokemon" label="pokemon"></v-text-field>
        <v-btn @click="search"
          ><v-icon>mdi-google-downasaur</v-icon> search</v-btn
        >
      </v-col>
      <v-col cols="12" offset-md="4">
        <v-card max-width="300">
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
      pokemon: undefined,
      res: undefined,
      pic: undefined,
      test: false,
    }
  },
  methods: {
    async search() {
      const poke = this.pokemon.toLowerCase()
      this.res = await this.$axios.$get(
        `https://pokeapi.co/api/v2/pokemon/${poke}`
      )
      this.pic = `https://pokeres.bastionbot.org/images/pokemon/${this.res.id}.png`
      this.test = true
    },
  },
}
</script>

<style></style>
