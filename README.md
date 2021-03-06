# React Blockly Drawer
A React component to play with blockly.
## Example

```shell 
$ npm install react-blockly-drawer node-blockly --save
```

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import Blockly from 'node-blockly/browser'; 

import BlocklyDrawer from 'react-blockly-drawer';
  
  const helloWorld =  {
    name: 'HelloWorld',
    category: 'Demo',
    block: {
      init: function () {
        this.jsonInit({
          message0: 'Hello %1',
          args0: [
            {
              type: 'field_input',
              name: 'NAME',
              check: 'String',
            },
          ],
          output: 'String',
          colour: 160,
          tooltip: 'Says Hello',
        });
      },
    },
    generator: (block) => {
      const message = `'${block.getFieldValue('NAME')}'` || '\'\'';
      const code = `console.log('Hello ${message}')`;
      return [code, Blockly.JavaScript.ORDER_MEMBER];
    },
  };

  ReactDOM.render(
    <BlocklyDrawer
      tools={[helloWorld]}
      onChange={(code, workspace) => {
        console.log(code, workspace);
      }}
    >
      <category name="Variables" custom="VARIABLE" />
      <category name="Values">
        <block type="math_number" />
        <block type="text" />
      </category>
    </BlocklyDrawer>,
    document.getElementById('root')
);

```

## Component Properties

#### `onChange`: function (code, workspaceXML) {}
Event listener to the workspace change.  Two arguments are passed to this callback:
- `code` that is the generated code of your created program.
- `workspaceXML` that is an XML text that corresponds to the content of the workspace.

#### `children`:  node(s)
Blockly predefined blocks/tools can be passed as children of this component.
For example, the following content could be passed.
```xml
<category name="Variables" custom="VARIABLE" />
<category name="Values">
  <block type="math_number" />
  <block type="text" />
</category>
```

#### `workspaceXML`: string [optional]
Workspace XML initial content. It is no necessary to pass it if you want a new/empty workspace.

#### `tools`: array [optional]
An array of your custom block/tools.
Each item should have the following properties:
 + ##### `name`: string
 + It is the name of the block/tool.
  
 + ##### `category`: string
 + The category where this block/tool is going to be inside of.
  
 + ##### `block`: object
 + Block's definition as it is done in Blockly.
 
 + ##### `generator`: function
 + Generator's definition as it is done in Blockly.
 
 
 For example:
 
 ```javascript
   {
      name: 'HelloWorld',
      category: 'Demo',
      block: {
        init: function () {
          this.jsonInit({
            message0: 'Hello %1',
            args0: [
              {
                type: 'field_input',
                name: 'NAME',
                check: 'String',
              },
            ],
            output: 'String',
            colour: 160,
            tooltip: 'Says Hello',
          });
        },
      },
      generator: (block) => {
        const message = `'${block.getFieldValue('NAME')}'` || '\'\'';
        const code = `console.log('Hello ${message}')`;
        return [code, Blockly.JavaScript.ORDER_MEMBER];
      },
    }
 ```

## Comments
Feel free to make any suggestion to improve this component.

