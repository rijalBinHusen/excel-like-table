<template>
    <div class="handsontable" id="example">
    <table class="htCore">
      <colgroup>
        <col  v-for="head in headers" :key="head" style="width: 200px">
      </colgroup>

      <thead>
        <tr>
          <th v-for="(head, index) in headers" :key="head">
            <div class="relative">
              <span :id="index" class="colHeader">{{ head }}</span>
            </div>
          </th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="(list, index) in lists" :key="list[keys[0]]" >
          <td v-for="(key, index2) in keys" :key="key" class="">
              <input @click="position(index, index2)" size="103" :id="'input'+index + index2" type="text" :value="list[key]">
            </td>
        </tr>  
      </tbody>
    </table>
  </div>

</template>

<script>
/* <ExcelTable 
    :headers="['Nama', 'Keterangan']" 
    :lists="[{name:1, keterangan:1}]" 
    :keys="['name', 'keterangan']"
    options
    />
*/
export default {
    data() {
        return {
            positionCol: 0,
            positionRow: 0,
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
            keyPress: {},
        }
    },
    methods: {
      position(row, col) {
        if(row === "bottomRight") {
          this.positionCol = this.headers.length
          this.positionRow = this.lists.length - 1
          return
        }

        if(row === "upLeft") {
          this.positionCol = 0
          this.positionRow = 0
          return
        }

        this.positionCol = col
        this.positionRow = row
      },

      focusNow() {
        document.getElementById(`input${this.positionRow+""+this.positionCol}`).focus()
      },

      releaseKey(event) {
        delete this.keyPress[event.key]
      },

      pressKey(event) {
        this.keyPress[event.key] = true

        if(this.keyPress.Control && this.keyPress.ArrowRight) {
          console.log("Control + Arah kanan")
          return
        }

        if(this.keyPress.Control && this.keyPress.ArrowLeft) {
          console.log("Control + Arah Kiri")
          return
        }

        if(this.keyPress.Control && this.keyPress.ArrowUp) {
          console.log("Control + Arah Atas")
          return
        }

        if(this.keyPress.Control && this.keyPress.ArrowDown) {
          console.log("Control + Arah bawah")
          return
        }

        if(this.keyPress.Shift && this.keyPress.Enter) {
          console.log("Shift + Enter")
          return
        }

        // Arrow left
        if(this.keyPress.ArrowLeft) {
          // mentok diatas
          let up = this.positionCol === 0
          // mentok dikiri
          let left = this.positionRow === 0
          //jika sudah mentok diatas kiri
          if(left && up) {
            //akhir cell = panjang heads + panjang row
            this.position("bottomRight")
          }
          //jika sudah mentok dikiri
          else if(left) {
            //naik ke atas, row - 1
            this.positionRow = this.positionRow - 1
            this.positionCol = this.headers.length - 1
          }
          //normal
          else {
            this.positionCol = this.positionCol - 1
          }
          this.focusNow()
        }

        // Arrow right
        if(this.keyPress.ArrowRight) {
          // mentok bawah
          let bottom = this.positionRow === (this.lists.length -1)
          // mentok kanan
          let right = this.positionCol === (this.headers.length -1)
          //jika sudah mentok dibawah kanan
          if(bottom && right) {
            this.position("upLeft")
          }
          //jika sudah mentok kanan
          else if(right) {
            //turun kebawah, row + 1
            this.positionRow = this.positionRow + 1
            this.positionCol = 0
          }
          //normal
          else {
            this.positionCol = this.positionCol + 1
          }
          this.focusNow()
        }

        //Arrow up
        if(this.keyPress.ArrowUp) {
          // jika tidak mentokk atas
          if(this.positionRow !== 0) {
            this.positionRow = this.positionRow - 1
          }
          this.focusNow()
        }

        if(this.keyPress.ArrowDown) {
          console.log("Arah bawah")
          return
        }

        if(this.keyPress.F2) {
          console.log("F2")
          return
        }

        if(this.keyPress.Home) {
          console.log("Home")
          return
        }

        if(this.keyPress.End) {
          console.log("End")
          return
        }

        if(this.keyPress.Enter) {
          console.log("Enter")
          return
        }
      }

    },
    mounted() {
        window.addEventListener("keydown", this.pressKey)
        window.addEventListener("keyup", this.releaseKey)
    },
    computed: {
      // longestString() {
      //    {
      //       name: {
      //         length: 70,
      //         index: 3
      //       }
      //       email: {
      //         length: 80,
      //         index: 3
      //       }
      //   */
      //  let result = {}
      //  this.headers.forEach((val) => {
      //    result.push(val.length)
      //  })
      //  this.lists.forEach((val) => {
      //    this.keys.forEach((key) => {
      //      val[key].length
      //    })
      //  })
      // }
    },
    unmounted() {
        window.removeEventListener("keydown", this.pressKey)
        window.removeEventListener("keyup", this.releaseKey)
    }
}
</script>

<style scoped>
.handsontable {
  position: relative;
}

.handsontable.htAutoColumnSize {
  visibility: hidden;
  left: 0;
  position: absolute;
  top: 0;
}

.handsontable table,
.handsontable tbody,
.handsontable thead,
.handsontable td,
.handsontable th,
.handsontable div {
  box-sizing: content-box;
  -webkit-box-sizing: content-box;
  -moz-box-sizing: content-box;
}

.handsontable table.htCore {
  border-collapse: separate;
  /*it must be separate, otherwise there are offset miscalculations in WebKit: http://stackoverflow.com/questions/2655987/border-collapse-differences-in-ff-and-webkit*/
  position: relative;
  /*this actually only changes appearance of user selection - does not make text unselectable
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -o-user-select: none;
  -ms-user-select: none;
  /*user-select: none; /*no browser supports unprefixed version*/
  border-spacing: 0;
  margin: 0;
  border-width: 0;
  table-layout: fixed;
  width: 0;
  outline-width: 0;
  /* reset bootstrap table style. for more info see: https://github.com/warpech/jquery-handsontable/issues/224 */
  max-width: none;
  max-height: none;
}

.handsontable col {
  width: 50px;
}

.handsontable col.rowHeader {
  width: 50px;
}

.handsontable th,
.handsontable td {
  border-right: 1px solid #CCC;
  border-bottom: 1px solid #CCC;
  height: 22px;
  empty-cells: show;
  line-height: 21px;
  padding: 0 4px 0 4px;
  /* top, bottom padding different than 0 is handled poorly by FF with HTML5 doctype */
  background-color: #FFF;
  vertical-align: top;
  overflow: hidden;
  outline-width: 0;
  white-space: pre-line;
  /* preserve new line character in cell */
}

.handsontable td.htInvalid {
  -webkit-transition: background 0.75s ease;
  transition: background 0.75s ease;
  background-color: #ff4c42;
}

.handsontable th:last-child {
  /*Foundation framework fix*/
  border-right: 1px solid #CCC;
  border-bottom: 1px solid #CCC;
}

.handsontable tr:first-child th.htNoFrame,
.handsontable th:first-child.htNoFrame,
.handsontable th.htNoFrame {
  border-left-width: 0;
  background-color: white;
  border-color: #FFF;
}

.handsontable th:first-child,
.handsontable td:first-child,
.handsontable .htNoFrame + th,
.handsontable .htNoFrame + td {
  border-left: 1px solid #CCC;
}

.handsontable tr:first-child th,
.handsontable tr:first-child td {
  border-top: 1px solid #CCC;
}

.handsontable thead tr:last-child th {
  border-bottom-width: 0;
}

.handsontable thead tr.lastChild th {
  border-bottom-width: 0;
}

.handsontable th {
  background-color: #EEE;
  color: #222;
  text-align: center;
  font-weight: normal;
  white-space: nowrap;
}

.handsontable thead th {
  padding: 0;
}

.handsontable th.active {
  background-color: #CCC;
}

.handsontable thead th .relative {
  position: relative;
  padding: 2px 4px;
}

/* plugins */

.handsontable .manualColumnMover {
  position: absolute;
  left: 0;
  top: 0;
  background-color: transparent;
  width: 5px;
  height: 25px;
  z-index: 999;
  cursor: move;
}

.handsontable th .manualColumnMover:hover,
.handsontable th .manualColumnMover.active {
  background-color: #88F;
}

.handsontable .manualColumnResizer {
  position: absolute;
  top: 0;
  cursor: col-resize;
}

.handsontable .manualColumnResizerHandle {
  background-color: transparent;
  width: 5px;
  height: 25px;
}

.handsontable .manualColumnResizer:hover .manualColumnResizerHandle,
.handsontable .manualColumnResizer.active .manualColumnResizerHandle {
  background-color: #AAB;
}

.handsontable .manualColumnResizerLine {
  position: absolute;
  right: 0;
  top: 0;
  background-color: #AAB;
  display: none;
  width: 0;
  border-right: 1px dashed #777;
}

.handsontable .manualColumnResizer.active .manualColumnResizerLine {
  display: block;
}

.handsontable .columnSorting:hover {
  text-decoration: underline;
  cursor: pointer;
}

/* border line */

.handsontable .wtBorder {
  position: absolute;
  font-size: 0;
}

.handsontable td.area {
  background-color: #EEF4FF;
}

/* fill handle */

.handsontable .wtBorder.corner {
  font-size: 0;
  cursor: crosshair;
}

.handsontable .htBorder.htFillBorder {
  background: red;
  width: 1px;
  height: 1px;
}

.handsontableInput {
  border: 2px solid #5292F7;
  outline-width: 0;
  margin: 0;
  padding: 1px 4px 0 2px;
  font-family: Arial, Helvetica, sans-serif;
  /*repeat from .handsontable (inherit doesn't work with IE<8) */
  line-height: 1.3em;
  /*repeat from .handsontable (inherit doesn't work with IE<8) */
  font-size: inherit;
  -webkit-box-shadow: 1px 2px 5px rgba(0, 0, 0, 0.4);
  box-shadow: 1px 2px 5px rgba(0, 0, 0, 0.4);
  resize: none;
  /*below are needed to overwrite stuff added by jQuery UI Bootstrap theme*/
  display: inline-block;
  color: #000;
  border-radius: 0;
  background-color: #FFF;
  /*overwrite styles potentionally made by a framework*/
}

.handsontableInputHolder {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 100;
}

.htSelectEditor {
  -webkit-appearance: menulist-button !important;
  position: absolute;
}

/*
TextRenderer readOnly cell
*/

.handsontable .htDimmed {
  color: #777;
}

/*
TextRenderer placeholder value
*/

.handsontable .htPlaceholder {
  color: #999;
}

/*
AutocompleteRenderer down arrow
*/

.handsontable .htAutocompleteArrow {
  float: right;
  font-size: 10px;
  color: #EEE;
  cursor: default;
  width: 16px;
  text-align: center;
}

.handsontable td .htAutocompleteArrow:hover {
  color: #777;
}

/*
CheckboxRenderer
*/

.handsontable .htCheckboxRendererInput.noValue {
  opacity: 0.5;
}

/*
NumericRenderer
*/

.handsontable .htNumeric {
  text-align: right;
}

/*context menu rules*/

ul.context-menu-list {
  color: black;
}

ul.context-menu-list li {
  margin-bottom: 0;
  /*Foundation framework fix*/
}

/**
 * dragdealer
 */

.handsontable .dragdealer {
  position: relative;
  width: 9px;
  height: 9px;
  background: #F8F8F8;
  border: 1px solid #DDD;
}

.handsontable .dragdealer .handle {
  position: absolute;
  width: 9px;
  height: 9px;
  background: #C5C5C5;
}

.handsontable .dragdealer .disabled {
  background: #898989;
}

/**
 * Handsontable in Handsontable
 */

.handsontable .handsontable .wtHider {
  padding: 0 0 5px 0;
}

.handsontable .handsontable table {
  -webkit-box-shadow: 1px 2px 5px rgba(0, 0, 0, 0.4);
  box-shadow: 1px 2px 5px rgba(0, 0, 0, 0.4);
}

/**
 * Handsontable listbox theme
 */

.handsontable.listbox {
  margin: 0;
}

.handsontable.listbox table {
  border: 1px solid #ccc;
  border-collapse: separate;
  background: white;
}

.handsontable.listbox th,
.handsontable.listbox tr:first-child th,
.handsontable.listbox tr:last-child th,
.handsontable.listbox tr:first-child td,
.handsontable.listbox td {
  border-width: 0;
}

.handsontable.listbox th,
.handsontable.listbox td {
  white-space: nowrap;
  text-overflow: ellipsis;
}

.handsontable.listbox td.htDimmed {
  cursor: default;
  color: inherit;
  font-style: inherit;
}

.handsontable.listbox .wtBorder {
  visibility: hidden;
}

.handsontable.listbox tr td.current,
.handsontable.listbox tr:hover td {
  background: #eee;
}

.htContextMenu {
  display: none;
  position: absolute;
}

.htContextMenu table.htCore {
  outline: 1px solid #bbb;
}

.htContextMenu .wtBorder {
  visibility: hidden;
}

.htContextMenu table tbody tr td {
  background: white;
  border-width: 0;
  padding: 4px 6px 0px 6px;
  cursor: pointer;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.htContextMenu table tbody tr td:first-child {
  border: 0;
}

.htContextMenu table tbody tr td.htDimmed{
  font-style: normal;
  color: #323232;
}

.htContextMenu table tbody tr td.current{
  background: rgb(233, 233, 233);
}

.htContextMenu table tbody tr td.htSeparator {
  border-top: 1px solid #bbb;
  height: 0;
  padding: 0;
}

.htContextMenu table tbody tr td.htDisabled {
  color: #999;
}

.htContextMenu table tbody tr td.htDisabled:hover {
  background: white;
  color: #999;
  cursor: default;
}

.handsontable td.htSearchResult {
  background: #fcedd9;
  color: #583707;
}

/*WalkontableDebugOverlay*/

.wtDebugHidden {
  display: none;
}

.wtDebugVisible {
  display: block;
  -webkit-animation-duration: 0.5s;
  -webkit-animation-name: wtFadeInFromNone;
  animation-duration: 0.5s;
  animation-name: wtFadeInFromNone;
}

@keyframes wtFadeInFromNone {
  0% {
    display: none;
    opacity: 0;
  }

  1% {
    display: block;
    opacity: 0;
  }

  100% {
    display: block;
    opacity: 1;
  }
}

@-webkit-keyframes wtFadeInFromNone {
  0% {
    display: none;
    opacity: 0;
  }

  1% {
    display: block;
    opacity: 0;
  }

  100% {
    display: block;
    opacity: 1;
  }
  
  
}

.handsontable tbody td {
  margin:0; padding:0;
  padding-right:12px;
}

input {
  border:none;
  width:100%;
  height:100%;
  font-family: Verdana, Helvetica, Arial, FreeSans, sans-serif;
  font-size:12px;
  padding: 0 4px 0 4px;
  
}

input:focus { 
  border:2px solid #5292F7;
  outline: none;
}

</style>