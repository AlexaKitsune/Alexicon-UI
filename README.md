# Alexicon-UI

Currently, the following types of components are available:

### Basic:

- text
- textarea
- button
- range
- checkbox
- switch
- radio
- color
- knob
- micro knob
- video
- audio
- code
- markdown
- window
- doc

### Advanced:

- mainpage
- searchbar

# Import

These can be invoked by importing the AlexiconComponent component and specifying the type:

```js
import AlexiconComponent from './AlexiconComponents/AlexiconComponent.vue';
```

### Basic:
```xml
<AlexiconComponent :type="'text'"/>
<AlexiconComponent :type="'textarea'"/>
<AlexiconComponent :type="'button'"></AlexiconComponent>
<AlexiconComponent :type="'range'"/>
<AlexiconComponent :type="'checkbox'"/>
<AlexiconComponent :type="'switch'"/>
<AlexiconComponent :type="'radio'"/>
<AlexiconComponent :type="'color'"/>
<AlexiconComponent :type="'knob'"/>
<AlexiconComponent :type="'microknob'"/>
<AlexiconComponent :type="'audio'"/>
<AlexiconComponent :type="'video'"/>
<AlexiconComponent :type="'code'"/>
<AlexiconComponent :type="'markdown'"/>
<AlexiconComponent :type="'window'"></AlexiconComponent>
<AlexiconComponent :type="'doc'"/>
```

### Advanced:
```xml
<AlexiconComponent :type="'mainpage'"></AlexiconComponent>
<AlexiconComponent :type="'searchbar'"></AlexiconComponent>
```

Notice how some components have both an opening and a closing tag.
This allows you to place content inside, just like a regular tag.

# Attributes

Each component has different attributes, some optional and some required.
Below are the characteristics of each one for each component type:

### Basic:

#### TEXT
```xml
<AlexiconComponent :type="'text'"/>
```
| Attribute         | Type               |
|-------------------|--------------------|
| `:val=""`         | String (optional)  |
| `:placeholder=""` | String (optional)  |
| `:disabled=""`    | Boolean (optional) |

#### TEXTAREA
```xml
<AlexiconComponent :type="'textarea'"></AlexiconComponent>
```
| Attribute         | Type               |
|-------------------|--------------------|
| `:val=""`         | String (optional)  |
| `:placeholder=""` | String (optional)  |
| `:disabled=""`    | Boolean (optional) |
| `:standalone=""`  | Boolean (optional) |
| `:resize=""`      | Boolean (optional) |

#### BUTTON
```xml
<AlexiconComponent :type="'button'"></AlexiconComponent>
```
| Attribute      | Type               |
|----------------|--------------------|
| `:disabled=""` | Boolean (optional) |

#### RANGE
```xml
<AlexiconComponent :type="'range'"/>
```
| Attribute      | Type               |
|----------------|--------------------|
| `:val=""`      | Number (optional)  |
| `:min=""`      | Number (optional)  |
| `:max=""`      | Number (optional)  |
| `:step=""`     | Number (optional)  |
| `:disabled=""` | Boolean (optional) |

#### CHECKBOX
```xml
<AlexiconComponent :type="'checkbox'"/>
```
| Attribute      | Type               |
|----------------|--------------------|
| `:checked=""`  | Boolean (optional) |
| `:disabled=""` | Boolean (optional) |

#### SWITCH
```xml
<AlexiconComponent :type="'switch'"/>
```
| Attribute      | Type               |
|----------------|--------------------|
| `:checked=""`  | Boolean (optional) |
| `:disabled=""` | Boolean (optional) |
        
#### RADIO
```xml
<AlexiconComponent :type="'radio'"/>
```
| Attribute      | Type               |
|----------------|--------------------|
| `:checked=""`  | Boolean (optional) |
| `:disabled=""` | Boolean (optional) |

#### COLOR
```xml
<AlexiconComponent :type="'color'"/>
```
| Attribute        | Type               |
|------------------|--------------------|
| `:val=""`        | String (optional)  |
| `:standalone=""` | Boolean (optional) |

#### KNOB
```xml
<AlexiconComponent :type="'knob'"/>
```
| Attribute      | Type               |
|----------------|--------------------|
| `:val=""`      | Number (optional)  |
| `:step=""`     | Number (optional)  |
| `:disabled=""` | Boolean (optional) |

#### MICRO KNOB
```xml
<AlexiconComponent :type="'microknob'"/>
```
| Attribute      | Type               |
|----------------|--------------------|
| `:val=""`      | Number (optional)  |
| `:step=""`     | Number (optional)  |
| `:disabled=""` | Boolean (optional) |

#### VIDEO
```xml
<AlexiconComponent :type="'video'"/>
```
| Attribute       | Type               |
|-----------------|--------------------|
| `:src=""`       | String             |
| `:autoplay=""`  | Boolean (optional) |
| `:loop=""`      | Boolean (optional) |
| `:framerate=""` | Number (optional)  |
| `:subtitles=""` | String (optional)  |

#### AUDIO
```xml
<AlexiconComponent :type="'audio'"/>
```
| Attribute      | Type               |
|----------------|--------------------|
| `:src=""`      | String             |
| `:autoplay=""` | Boolean (optional) |
| `:loop=""`     | Boolean (optional) |

#### CODE
```xml
<AlexiconComponent :type="'code'"/>
```
| Attribute | Type   |
|-----------|--------|
| `:val=""` | String |

#### MARKDOWN
```xml
<AlexiconComponent :type="'markdown'"/>
```
| Attribute | Type   |
|-----------|--------|
| `:val=""` | String |

#### WINDOW
```xml
<AlexiconComponent :type="'window"></AlexiconComponent>
```
| Attribute             | Type             |
|-----------------------|------------------|
| `:title=""`           | any (optional)   |
| `:initialPosition=""` | Array (optional) |

#### DOC
```xml
<AlexiconComponent :type="'doc'"/>
```
| Attribute | Type   |
|-----------|--------|
| `:src=""` | String |

### Advanced:

#### MAIN PAGE
```xml
<AlexiconComponent :type="'mainpage'"></AlexiconComponent>
```
_No attributes_.

#### SEARCH BAR
```xml
<AlexiconComponent :type="'searchbar'"></AlexiconComponent>
```
| Attribute         | Type               |
|-------------------|--------------------|
| `:val=""`         | String (optional)  |
| `:placeholder=""` | String (optional)  |
| `:disabled=""`    | Boolean (optional) |
| `"bgcolor=""`     | Array (optional)   |

# Get data

Data capture is performed through the `@get-value=""` event, which is triggered whenever the input value changes.

For example, using a text input component:

```xml
<AlexiconComponent :type="'text'"
    :placeholder="'Type something...'"
    @get-val="(val) => myFunction(val, 'txtexample')"
/>
```

Where `myFunction` can be any custom function that we can create. In this example, we'll define it like this:

```js
myFunction(val, orig) {
    console.log("getting value:", val, orig);
}
```

When executed (typing "Hello world"), it will print the following in the console:

```
getting value: Hello world txtexample
```

This `@get-value=""` event is only available in the following components:

- text
- textarea
- range
- checkbox
- switch
- radio
- color
- knob
- micro knob

However, there are some specific events for specific components:

#### VIDEO
| Event                  | |
|------------------------|-|
| `@get-play-pause=""`   | |
| `@get-current-time=""` | |
| `@get-play-seek=""`    | |
| `@get-play-cc=""`      | |
| `@get-play-loop=""`    | |

#### AUDIO
| Event                  | |
|------------------------|-|
| `@get-play-pause=""`   | |
| `@get-current-time=""` | |
| `@get-play-seek=""`    | |
| `@get-play-loop=""`    | |

#### SEARCH BAR
| Event                 | |
|-----------------------|-|
| `@get-switch-menu=""` | |

# Advanced components structures

```xml
<AlexiconComponent :type="'mainpage'">
    <AlexiconComponent :type="'searchbar'" @get-switch-menu="(val) => menuActive = val"></AlexiconComponent>
    <div class="Alexicon-container">
        <AlexiconComponent :type="'asidemenu'" :active="menuActive"></AlexiconComponent>
        <main class="Alexicon-main">
            (content...)
        </main>
    </div>
</AlexiconComponent>
```
```
npm i highlight.js
npm i mammoth
npm i xlsx
npm i marked
npm i marked-katex-extension
npm i marked-highlight
npm i srt-parser-2
npm i lucide-vue-next
```