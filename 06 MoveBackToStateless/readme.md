# 06 MoveBackToStateless

In example 05 we learned how to remove state from a child control just to have clear governance of state.

It's time to make some cleanup, let's simplify _[nameEdit.tsx](./src/nameEdit.tsx)_ component and modify it to a stateless component.

We take _[05 Refactor](./../05%20Refactor)_ as reference.

Summary steps:

- Update _[nameEdit.tsx](./src/nameEdit.tsx)_ and modify it to a stateless component.

## Prerequisites

Install [Node.js and npm](https://nodejs.org/en/) (v6.6.0 or newer) if they are not already installed on your computer.

> Verify that you are running at least node v6.x.x and npm 3.x.x by running `node -v` and `npm -v` in a terminal/console window. Older versions may produce errors.

## Steps to build it

- Copy the content from _[05 Refactor](./../05%20Refactor)_ and execute `npm install`.

- Update _[nameEdit.tsx](./src/nameEdit.tsx)_ and modify it to stateless component. It should look like this:

 ```jsx
import * as React from 'react';
import {Fragment} from 'react';


interface Props {
    editingUserName : string;
    onEditingNameUpdated : (newEditingName : string) => void;
    onNameUpdateRequest : () => void;  
}

  
export const NameEditComponent = (props : Props) =>
  <div>
      <label>Update Name:</label>
      <input value={props.editingUserName}
        onChange={(e) : void => props.onEditingNameUpdated((e.target as HTMLInputElement).value)} />

      <button className="btn btn-default" onClick={props.onNameUpdateRequest}>Change</button>
  </div>
 ```

Side note: during the refactory we have changed ```this.props``` to ```props```. This is a required step as ```NameEditComponent``` is no longer a class but a function. During runtime, ```this``` is now undefined, so obviously then ```this.props``` fails.

Side note 2: applying currying and Fragments, the code for ```NameEditComponent``` looks like this:

```
const onChange = (props: Props) => (event) => {
  props.onEditingNameUpdated(event.target.value)
}

export const NameEditComponent = (props : Props) =>
  <>
      <label>Update Name:</label>
      <input value={props.editingUserName} onChange={onChange(props)} />
      <button className="btn btn-default" onClick={props.onNameUpdateRequest}>Change</button>
  </>
 ```
- Now we can run the example and we get the same results

```bash
npm start
```
