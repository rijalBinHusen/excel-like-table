<template>
    <div class="countDown">{{ countDown ? "Data would auto save in "+ countDown + " second" : "Nothing change" }}</div>
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
        <tr v-for="(list, index) in lists" :key="list" >
          <td v-for="(key, index2) in keys" :key="key">
              <input  
                type="text" 
                :id="'input'+index + index2" 
                v-model="list[key]"
                :readonly="!edit"
                @click="position(index, index2)"
                @change="changed(index)"
              >
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
  />
*/
export default {
    data() {
        return {
            positionCol: 0,
            positionRow: 0,
            keyPress: {},
            edit: false,
            changedRow: [],
            countDown: 0,
            count: null,
        }
    },
    props: {
      headers: {
        type: Array,
        required: true,
      },
      lists: {
        type: Array,
        required: true,
      },
      keys: {
        type: Array,
        required: true,
      }
    },
    emits: ["changed"],
    methods: {
      changed(ev) {
        console.log(ev)
        this.edit = false
        for(let i = 0; i < this.headers.length; i++) {
          document.getElementById(`input${ev+""+i}`).style.fontWeight = "bold"
        }
        if(!this.changedRow.includes(ev)) {
          this.changedRow.push(ev)
        }
        this.startCountDown()
      },
      startCountDown() {
        clearInterval(this.count)
        this.reduceCount("start")
        this.count = setInterval(() => { this.reduceCount() }, 1000)
      },
      reduceCount(ev) {
        if(ev == "start") {
          this.countDown = 10
          return
        } if(!this.countDown) {
          console.log("selesai")
          this.$emit("changed", this.changeRow)
          clearInterval(this.count)
          return
        }
        this.countDown = this.countDown - 1
      },
      position(row, col) {
        this.positionCol = col
        this.positionRow = row
      },

      focusNow() {
        document.getElementById(`input${this.positionRow+""+this.positionCol}`).focus()
      },

      goLeft() {
        if(this.positionCol !== 0) {
          this.positionCol = this.positionCol - 1
          return
        }
        this.goUpRow()
        this.goEndCol()
      },
      goRight() {
        if(this.positionCol !== (this.headers.length -1)) {
          this.positionCol = this.positionCol + 1
          return
        }
        this.goDownRow()
        this.goBeginCol()
      },
      goBeginCol() {
        this.positionCol = 0
      },
      goEndCol() {
        this.positionCol = this.headers.length - 1
      },
      goUpRow(){
        if(this.positionRow !== 0) {
          this.positionRow = this.positionRow - 1
          return
        }
        this.goEndRow()
      },
      goDownRow(){
        if(this.positionRow !== (this.lists.length - 1)) {
          this.positionRow = this.positionRow + 1
          return
        }
        this.goBeginRow()
      },
      goBeginRow() {
        this.positionRow = 0
      },
      goEndRow() {
        this.positionRow = this.lists.length - 1
      },
      releaseKey(event) {
        this.focusNow()
        delete this.keyPress[event.key]
      },

      pressKey(event) {
        this.keyPress[event.key] = true

        if(this.keyPress.Control && this.keyPress.ArrowRight) {
          this.goEndCol()
          return
        }

        if(this.keyPress.Control && this.keyPress.ArrowLeft) {
          this.goBeginCol()
          return
        }

        if(this.keyPress.Control && this.keyPress.ArrowUp) {
          this.goBeginRow()
          return
        }

        if(this.keyPress.Control && this.keyPress.ArrowDown) {
          this.goEndRow()
          return
        }

        if(this.keyPress.Shift && this.keyPress.Enter) {
          this.goUpRow()
          return
        }

        // Arrow left
        if(this.keyPress.ArrowLeft) {
          this.goLeft()
          return
        }

        // Arrow right
        if(this.keyPress.ArrowRight) {
          this.goRight()
          return
        }

        //Arrow up
        if(this.keyPress.ArrowUp) {
          this.goUpRow()
          return
        }

        if(this.keyPress.ArrowDown) {
          this.goDownRow()
          return
        }

        if(this.keyPress.F2) {
          this.edit = true
          // this.focusNow()
          return
        }

        if(this.keyPress.Escape) {
          this.edit = false
          return
        }

        if(this.keyPress.Home) {
          this.goBeginCol()
          return
        }

        if(this.keyPress.End) {
          this.goEndCol()
          return
        }

        if(this.keyPress.Enter) {
          this.goDownRow()
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
  align-items: center;
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
  /* margin: 0;
   */
  margin-left: auto;
  margin-right: auto;
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

.countDown {
  position: relative;
  background-color: gray;
  padding: 15px;
  margin-bottom: 
  20px;opacity: 
  40%;font-size: 
  30px;
}

</style>