<template>
   <ExcelTable 
    :headers="headers" 
    :lists="lists" 
    :keys="keys"
    
  />
</template>

<script>
import ExcelTable from "./components/ExcelTable.vue"

export default {
  name: 'App',
  data() {
      return {
        headers: ["Nama", "Alamat Email", "Nomor telephone", "Kota"],
        lists: [
          {
            "name": "Melodie Larsen",
            "email": "dolor.dapibus@hotmail.ca",
            "phone": "(620) 908-4668",
            "city": "26722"
          },
          {
            "name": "Shaeleigh Conway",
            "email": "lorem.auctor.quis@protonmail.com",
            "phone": "(484) 184-0810",
            "city": "15388"
          },
          {
            "name": "Faith Michael",
            "email": "adipiscing.enim@google.ca",
            "phone": "1-237-448-3180",
            "city": "261295"
          },
          {
            "name": "Clare Rosa",
            "email": "cum@outlook.net",
            "phone": "(468) 960-8712",
            "city": "0719"
          },
          {
            "name": "Dawn Bridges",
            "email": "cras@protonmail.org",
            "phone": "(450) 450-7712",
            "city": "3375"
          },
          {
            "name": "Mark Olson",
            "email": "at.pede@icloud.com",
            "phone": "1-256-654-4911",
            "city": "T7K 3Y2"
          },
          {
            "name": "Anthony Boyd",
            "email": "nam.tempor@google.couk",
            "phone": "(718) 471-7632",
            "city": "85724-319"
          },
          {
            "name": "Sydnee Vinson",
            "email": "convallis.in@hotmail.org",
            "phone": "(633) 378-2278",
            "city": "1101"
          },
          {
            "name": "Sade Key",
            "email": "pede.nunc@hotmail.edu",
            "phone": "(557) 778-7476",
            "city": "2654"
          },
          {
            "name": "Uriel Pickett",
            "email": "nunc.ut@hotmail.org",
            "phone": "1-461-363-6266",
            "city": "2975 HN"
          },
          {
            "name": "Kelsie Blake",
            "email": "nunc.quisque.ornare@outlook.edu",
            "phone": "(626) 137-3358",
            "city": "2382"
          },
          {
            "name": "Alma Reeves",
            "email": "inceptos.hymenaeos@hotmail.com",
            "phone": "(767) 397-8628",
            "city": "5667"
          },
          {
            "name": "Imelda House",
            "email": "erat.sed@google.net",
            "phone": "1-640-793-1223",
            "city": "886953"
          },
          {
            "name": "Lance Mckee",
            "email": "justo.eu.arcu@icloud.couk",
            "phone": "1-982-756-8823",
            "city": "13-091"
          },
          {
            "name": "Gemma Carey",
            "email": "sollicitudin.orci@aol.couk",
            "phone": "(647) 213-2723",
            "city": "50106"
          },
          {
            "name": "Amber Moss",
            "email": "nonummy.ac@protonmail.edu",
            "phone": "(972) 737-4138",
            "city": "762288"
          },
          {
            "name": "Mollie Whitley",
            "email": "nec@protonmail.org",
            "phone": "(544) 707-3871",
            "city": "72548-26307"
          },
          {
            "name": "Calista Sutton",
            "email": "vehicula.risus.nulla@aol.edu",
            "phone": "(539) 595-2744",
            "city": "88618"
          },
          {
            "name": "Andrew Hicks",
            "email": "rutrum@aol.edu",
            "phone": "(412) 841-9716",
            "city": "302128"
          },
          {
            "name": "Blythe Leon",
            "email": "in@hotmail.net",
            "phone": "(665) 227-1937",
            "city": "693412"
          }
        ],
        keys: ["name", "email", "phone", "city"],
      }
  },
  components: {
    ExcelTable
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
