### Convert Template String into Parsed String

```js
function parseTemplate(templateString, values) {
  let parsedString = templateString;
  for (const key in values) {
    parsedString = parsedString.replace(
      new RegExp(`\\{\\{${key}\\}\\}`, 'g'),
      values[key]
    );
  }
  return parsedString;
}

// Example usage
const output = parseTemplate('my name is {{name}}', { name: 'John' });
console.log(output); // Outputs: 'my name is John'
```

### Example 2 code

```js
function parseTemplate1(templateString, values) {
  return templateString.replace(/\{\{([\w.]+)\}\}/g, (match, key) => {
    // Split the key on dots to navigate through the nested objects
    return key.split('.').reduce((acc, k) => {
      return acc && acc[k] ? acc[k] : match;
    }, values);
  });
}

// Example usage
const output1 = parseTemplate1('Hello, {{user.name}}', {
  user: { name: 'John' },
});
console.log(output1); // Outputs: 'Hello, John'
```
