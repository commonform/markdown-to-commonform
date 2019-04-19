convert CommonMark to Common Form

```javascript
var toCommonForm = require('commonmark-to-commonform')
var assert = require('assert')

assert.deepEqual(
  toCommonForm(
    [
      '# Title',
      '',
      '## First Heading',
      '',
      'This is the **Agreement**.',
      '',
      '## Second Heading',
      '',
      'Using the term _Agreement_.',
      'Referencing [First Heading](#first-heading).',
    ].join('\n')
  ),
  {
    content: [
      {
        heading: 'First Heading',
        form: {
          content: ['This is the ', {definition: 'Agreement'}, '.']
        }
      },
      {
        heading: 'Second Heading',
        form: {
          content: [
            'Using the term ', {use: 'Agreement'}, '. ' +
            'Referencing ', {reference: 'First Heading'}, '.'
          ]
        }
      }
    ]
  }
)
```