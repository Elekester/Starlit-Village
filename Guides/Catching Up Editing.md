# Nel's Guide to Catching Up in PSO2: NGS Editing Notes

You can run this JavaScript code in your browser to generate the Table of Contents.

```JavaScript
console.log([...document.querySelectorAll('#readme h1, #readme h2')].map((header, index) => {
    if (index < 2) return '';
    headerTitle = header.innerText;
    headerUrl = headerTitle.replaceAll(' ', '-').replaceAll(':','');
    return '\t'.repeat(header.tagName[1] - 1) + '- ['+ headerTitle +'](#' + headerUrl + ')\n';
}).join(''));
```
