# Excel table like

I just wanna make html table but like excel style, just table only not the spreadsheet feature

---

## todo
- Keyboard event in spreadsheet style
  [x] Arrow right to navigation to right cell
  [x] Arrow left to navigation to the before cell
  [x] Arrow up to navigation to up cell
  [x] Arrow down to navigation to bottom cell
  [x] Home to the begin col
  [x] End navigation to the end col
  [x] Ctrl + Arrow right to navigation to the end col
  [x] Ctrl + Arrow left to navigation to the begin col
  [x] Ctrl + Arrow up to navigation to the end row
  [x] Ctrl + Arrow down to navigation to the begin row
  [x] Tab to the right cell
  [x] Shift + tab to the left cell
  [x] Enter to the bottom cell
  [x] Shift + enter to the up cell
  [ ] F2 to edit the cell (optional)

- [ ] width cell auto fit with the length string, wrap the text if width is on maximum
- [ ] Make row bold when the row changed
- [ ] Auto send an changed event to the parent component after 10 second of changed cell

# How to add this component to your project?

```
Just copy paste the raw of /src/components/ExcelTable.vue file
```

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
