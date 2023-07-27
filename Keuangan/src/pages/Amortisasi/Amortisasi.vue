<template>
  <q-page>
    <div class="flex tw-justify-center tw-my-8">
      <div>
        <ul>
          <li>
            <label for="">
              <q-input
                type="number"
                placeholder="nilai pembiayaan"
                v-model="pembiayaan"
                label="Pembiayaan"
              />
            </label>
          </li>
          <li>
            <label for="">
              <q-input
                type="number"
                placeholder="lama angsuran"
                v-model="n"
                label="Tenor"
              />
            </label>
          </li>
          <li>
            <label for="">
              <q-input
                type="number"
                placeholder="nilai bunga"
                v-model="bunga"
                label="Rate"
              />
            </label>
          </li>
        </ul>
        <div class="tw-my-4">
          <q-btn @click="getdata">calculate</q-btn>
          <q-btn @click="dataReset">reset</q-btn>
        </div>
      </div>
    </div>
    <div class="flex tw-justify-center tw-my-8">
      <ul>
        <h1 class="t tw-text-center">Hasil Perhitungan</h1>
        <li class="tw-my-3" v-for="(arr, index) in tempArr" :key="index">
          angsuranke : {{ arr.angsuranke }}, angsuran : {{ arr.angsuran }},
          bunga : {{ arr.bunga }}, pokok : {{ arr.pokok }}, osp : {{ arr.osp }}
        </li>
      </ul>
    </div>
  </q-page>
</template>
<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "AmortisasiMoney",
  setup() {
    return {
      pembiayaan: ref(0),
      bunga: ref(0),
      n: ref(0),
      tempArr: ref([]),
      tempObj: ref({
        angsuranke: 0,
        angsuran: 0,
        bunga: 0,
        pokok: 0,
        osp: 0,
      }),
    };
  },
  methods: {
    getPMT() {
      let p = this.pembiayaan;
      let r = this.bunga / 1200;
      let n = this.n;

      let pembagi = Math.pow(1 + r, n) - 1;
      let angsuran = (p * r * Math.pow(1 + r, n)) / pembagi;

      return parseFloat(angsuran.toFixed(3));
    },

    dataReset() {
      this.tempArr = [];
    },

    getdata() {
      let data = this.getPMT();
      let n = this.n;

      let p2 = this.pembiayaan;
      for (let i = 0; i < n; i++) {
        let rate = (p2 * this.bunga) / 1200;
        let principal = data - rate;
        let ospNew = Math.abs(p2 - principal);

        this.tempObj = {
          angsuranke: i + 1,
          angsuran: parseFloat(data.toFixed(3)),
          bunga: parseFloat(rate.toFixed(3)),
          pokok: parseFloat(principal.toFixed(3)),
          osp: parseFloat(ospNew.toFixed(3)),
        };

        p2 = ospNew;

        this.tempArr.push(this.tempObj);
        // console.log(this.tempArr);
      }
    },
  },
});
</script>
