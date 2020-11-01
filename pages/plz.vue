<template>
  <v-container fluid>
    <v-row align="center">
      <v-col class="d-flex" cols="12" sm="6">
        <v-select :items="items" label="Standard" dense></v-select>
      </v-col>

      <v-col class="d-flex" cols="12" sm="6">
        <v-select :items="items" filled label="Filled style" dense></v-select>
      </v-col>

      <v-col class="d-flex" cols="12" sm="6">
        <v-select
          :items="items"
          label="Outlined style"
          dense
          outlined
        ></v-select>
      </v-col>

      <v-col class="d-flex" cols="12" sm="6">
        <v-select :items="items" label="Solo field" dense solo></v-select>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      items: ['Foo', 'Bar', 'Fizz', 'Buzz'],
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
    }
  },
  methods: {},
}
</script>

<style></style>
