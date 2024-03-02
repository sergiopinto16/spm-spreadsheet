
1. Open google sheet link and create a copy in work workspace

https://docs.google.com/spreadsheets/d/1ZidSTm7qvHhGTbvoGMzxtlvIVPlyIsZfMMuRysv_36o/edit?usp=sharing


2. Add code scripts in Extensões -> Apps Scripts and add function code:
   
```
function clearCheckboxes() {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var range = sheet.getRange('F1:I150'); // Adjust the range as per your requirement
  
  var data = range.getValues();
  
  for (var i = 0; i < data.length; i++) {
    for (var j = 0; j < data[i].length; j++) {
      if (typeof data[i][j] === 'boolean') {
        range.getCell(i+1, j+1).setValue(false);
      }
    }
  }
}

// multiple checkboxs selected
function onEdit(e) {
  var sheet = e.source.getActiveSheet();
  var range = e.range;
  var row = range.getRow();
  var values = sheet.getRange(row, 6, 1, 5).getValues()[0];
  var checkboxes = values.map(function(value) {
    return value === true;
  });
  if (row < 150){
    if (checkboxes.filter(Boolean).length > 1) {
      sheet.getRange(row, 2, 1, 9).setBackground('red');
    } else {
      sheet.getRange(row, 2, 1, 9).setBackground(null);
    }
  }
}
```

3 . Link LIMPAR buttons to fucntion clearCheckboxes
