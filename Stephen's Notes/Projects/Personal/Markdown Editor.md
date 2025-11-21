Steps recommended by chatgpt:
- Parse the MD using `marked` 
- Add custom styles through the app using the dom
- Then use jsPDF to convert the html into js
```
const doc = new jsPDF();
doc.html(document.body, {
  callback: function (doc) {
    doc.save('styled-markdown.pdf');
  }
});
```
- SimpleMDE or CodeMirror allow for on the fly editing
- ![[Markdown Beautifier diagram.png]]