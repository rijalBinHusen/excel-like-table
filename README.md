# Excel table like

I just wanna make html table but like excel style, just table only not the spreadsheet feature

---

## todo
- [ ] Keyboard event in spreadsheet style
  [ ] Arrow right to navigation to right cell
  [x] Arrow left to navigation to the before cell
  [ ] Arrow up to navigation to up cell
  [ ] Arrow down to navigation to bottom cell
  [ ] Ctrl + Arrow right to navigation to the right end cell
  [ ] Ctrl + Arrow left to navigation to the left end cell
  [ ] Ctrl + Arrow up to navigation to the up end cell
  [ ] Ctrl + Arrow down to navigation to the bottom end cell
  [x] Tab to the right cell, **active by default**
  [x] Shift + tab to the left cell **active by default**
  [ ] Enter to the bottom cell
  [ ] Shift + enter to the up cell
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
