### React-Tags

[![NPM](https://nodei.co/npm/react-tag-input.png?downloads=true)](https://www.npmjs.com/package/react-tag-input)

React tags is a simple tagging component ready to drop in your React projects. The component is inspired by GMail's *To* field in the compose window.

### Features
- Autocomplete based on a suggestion list
- Keyboard friendly and mouse support

### Why
Because I was looking for an excuse to build a standalone component and publish it in the wild? To be honest, I needed a tagging component that provided the above features for my [React-Surveyman](http://github.com/prakhar1989/react-surveyman) project. Since I was unable to find one which met my requirements (and the fact that I generally enjoy re-inventing the wheel) this is what I came up with.


### Demo
![img](demo.gif)

Check it out [here](http://prakhar.me/react-tags/example)

### Installation
The preferred way of using the component is via NPM

```
npm install --save react-tag-input
```
It is, however, also available to be used separately (`dist/ReactTags.min.js`). If you prefer this method remember to include [ReactDND](https://github.com/gaearon/react-dnd) as a dependancy. Refer to the [demo](http://prakhar.me/react-tags/example) to see how this works.

### Usage

Here's a sample implementation that initializes the component with a list of initial `tags` and `suggestions` list. Apart from this, there are multiple events, handlers for which need to be set. For more details, go through the [API](#Options).

```javascript
var ReactTags = require('react-tag-input');

var App = React.createClass({
    getInitialState: function() {
        return {
            tags: [ {id: 1, text: "Apples"} ],
            suggestions: ["Banana", "Mango", "Pear", "Apricot"]
        }
    },
    handleDelete: function(i) {
        var tags = this.state.tags;
        tags.splice(i, 1);
        this.setState({tags: tags});
    },
    handleAddition: function(tag) {
        var tags = this.state.tags;
        tags.push({
            id: tags.length + 1,
            text: tag
        });
        this.setState({tags: tags});
    },
    render: function() {
        var tags = this.state.tags;
        var suggestions = this.state.suggestions;
        return (
            <div>
                <ReactTags tags={tags}
                    suggestions={suggestions}
                    handleDelete={this.handleDelete}
                    handleAddition={this.handleAddition} />
            </div>
        )
    }
});

React.render(<App />, document.getElementById('app'));
```

<a name="Options"></a>
### Options

- [`tags`](#tagsOption)
- [`suggestions`](#suggestionsOption)
- [`delimeters`](#delimeters)
- [`placeholder`](#placeholderOption)
- [`labelField`](#labelFieldOption)
- [`handleAddition`](#handleAdditionOption)
- [`handleDelete`](#handleDeleteOption)
- [`autofocus`](#autofocus)
- [`handleInputChange`](#handleInputChange)
- [`minQueryLength`](#minQueryLength)
- [`autocomplete`](#autocomplete)

<a name="tagsOption"></a>
##### tags (optional)
An array of tags that are displayed as pre-selected. Each tag should have an `id` and a `text` property which is used to display.

```js
var tags =  [ {id: 1, text: "Apples"} ]
```

<a name="suggestionsOption"></a>
##### suggestions (optional)
An array of suggestions that are used as basis for showing suggestions. At the moment, this should be an array of strings.

```js
var suggestions = ["mango", "pineapple", "orange", "pear"];
```

<a name="delimeters"></a>
##### delimeters (optional)
Specifies which characters should terminate tags input (default: enter and tab). A list of character codes.


<a name="placeholderOption"></a>
##### placeholder (optional)
The placeholder shown for the input. Defaults to `Add new tag`.

```
var placeholder = "Add new country"
```

<a name="labelFieldOption"></a>
##### labelField (optional)
Provide an alternative `label` property for the tags. Defaults to `text`.

```
<ReactTags tags={tags}
    suggestions={}
    labelField={'name'} />
```
This is useful if your data uses the `text` property for something else.


<a name="handleAdditionOption"></a>
##### handleAddition (required)
Function called when the user wants to add a tag (either a click, a tab press or carriage return)

```js
function(tag) {
    // add the tag to the tag list
}
```

<a name="handleDeleteOption"></a>
##### handleDelete (required)
Function called when the user wants to delete a tag

```js
function(i) {
    // delete the tag at index i
}
```

```js
function(tag, currPos, newPos) {
    // remove tag from currPos and add in newPos
}
```
<a name="autofocus"></a>
##### autofocus (optional)
Optional boolean param to control whether the text-input should be autofocused on mount.

```js
<ReactTags
    autofocus={false}
    ...>
```

<a name="handleInputChange"></a>
##### handleInputChange (optional)
Optional event handler for input onChange

```js
<ReactTags
    handleInputChange={this.handleInputChange}
    ...>
```

<a name="minQueryLength"></a>
##### minQueryLength (optional)
How many characters are needed for suggestions to appear (default: 2).

### Styling
`<ReactTags>` does not come up with any styles. However, it is very easy to customize the look of the component the way you want it. The component provides the following classes with which you can style -

- `ReactTags__tags`
- `ReactTags__tagInput`
- `ReactTags__selected`
- `ReactTags__selected ReactTags__tag`
- `ReactTags__selected ReactTags__remove`
- `ReactTags__suggestions`

An example can be found in `/example/reactTags.css`.

### Dev
The component is written in ES6 and uses [Webpack](http://webpack.github.io/) as its build tool.
```
npm install
npm run dev
python -m SimpleHTTPServer ### open in browser
```

### Contributing
Got ideas on how to make this better? Open an issue! I'm yet to add tests so keep your PRs on hold :grinning:

### Thanks
The autocomplete dropdown is inspired by Lea Verou's [awesomeplete](https://github.com/LeaVerou/awesomplete) library.
