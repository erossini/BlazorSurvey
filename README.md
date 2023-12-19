# Survey components for Blazor

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/4cb8e86c-aaf8-4d17-bf56-203a42397e12)

## Components

### Basic components

- [x] Textbox
- [x] Checkbox
- [x] Slider
- [x] Radiobutton
- [x] DropdownList
- [x] Comment
- [x] Boolean
- [x] ImagePicker
- [ ] UploadFile
- [X] HTML

### Group of components

- [x] Matrix (Single choice)
- [ ] Matrix (Multiple choices)
- [ ] Matrix Dynamic rows
- [ ] Multiple Textbox

### Custom components

- [x] NPS (Net Promoter Score)
- [x] Likert Skill
- [ ] Multiselect
- [ ] Semantic differential
- [x] Rating
- [ ] Ranking

### Group of elements

- [x] Panel
- [ ] Page
- [x] Repeater

## Properties

### Name

Each element has a property called `Name` that allows you to identify the element in the form. This property is required.

Apart from _panel_ and _repeater_ components, the element's name will be used to identify the element's value in the form.
The conventional name is formed by the prefix of the element and a progressive number.

For example, if you have in the form only one textbox, the conventional name will be `txt_1`, the value of the textbox will be stored in the form with the key `txt_1`.

To use custom a `Name`, in the `Survey` set to `False` the property `UseNamingComvention` of the survey component. For example:

```html
<Survey Form="form"
        ShowDebug="true"
        UseNamingComvention="false"
        OnFormValuesChanged="OnFormValuesChanges"
        OnFormSubmitted="OnFormSubmitted"
        OnFormSubmittedError="OnFormSubmittedError" />
```

By default the property `UseNamingComvention` is set to `True` and every component will be named based on the following convention

| Component   | Convention |
| ----------- | ---------- |
| Checkbox    | chk        |
| Comment     | cmt        |
| Dropdown    | ddl        |
| HTML        | htm        |
| LikertSkill | lks        |
| Matrix      | mtx        |
| NPS         | nps        |
| Panel       | pnl        |
| Radiobutton | rdb        |
| Rating      | rtn        |
| Repeater    | rpt        |
| Slider      | sld        |
| Switch      | swc        |
| TextBox     | txt        |

### VisibleIf

Each element has a property called `VisibleIf` that allows you to show or hide the element based on the value of another element.

To use this property, you must specify the `Name` of the element used to evaluate the condition and the `Value` that will be used to compare.
Also, you must set to `False` the property `UseNamingComvention` of the survey component.

#### Refer to a TextBox

When a field of the survey depends on a value on a `TextBox`, it is enough to write the condition with the name of the field and the value: the survey component will evaluate the condition and if the value of the `TextBox` is exactly the required value, the field will be displayed. For example:

```csharp
new Textbox() {
    Title = "First name (insert 1 to test the filters)",
    PlaceHolder = "Enter your name",
    Name = "txt1",
    IsRequired = true
},
new Textbox() {
    Title = "Middle name",
    PlaceHolder = "Enter your middle name",
    Name = "txt2",
    Description = "Insert your middle name",
    VisibleIf = "txt1 = '1'" },
```

The `TextBox` _txt2_ will be displayed if the value of the _txt1_ is equal to the string `1`. 

#### Refer to a Radiobutton

When a field has to depend on a `Radiobutton`, the value to be specified is the index of the element. For example:

```csharp
new Radiobutton() {
    Title = "This is a radiobutton",
    Description = "Select one of the following options",
    Name = "radio1", Choices = new List<object>() {
        "One", "Two", "Three",
        new RadiobuttonChoice() { Label = "Four" }
    },
    IsRequired = true
},
new Radiobutton() { 
    Title = "This is a radiobutton", 
    Description = "Select one of the following options",
    Name = "radio12", 
    Choices = new List<object>() {
        "One", "Two", "Three",
        new RadiobuttonChoice() { Label = "Four" }
    }, 
    VisibleIf = "radio1 = 1",
    IsRequired = true },
```

### Show debug section

The component has a section for debugging the creation of the form and its result. To disable the debug set to `False` the property `ShowDebug`. By default, this property is set to `True` and 2 sections are displayed at the bottom of the form:

- Json Form
- Json Result

#### Json Form

In this section, the `Survey` component displays the `json` to create the survey itself. This can be used to generate the form a run-time from a file or an API.

An example for the `json` is the following one:

```
{
  "elements": [
    {
      "type": "Checkbox",
      "choices": [
        "One",
        "Two",
        "Three",
        {
          "label": "Four"
        }
      ],
      "orientation": 1,
      "description": "Try to check more than one option",
      "isRequired": false,
      "isVisible": true,
      "name": "chk_1",
      "questionNumber": "1",
      "title": "This is a checkbox"
    },
    {
      "type": "Checkbox",
      "choices": [
        "One",
        "Two",
        "Three",
        {
          "label": "Four"
        }
      ],
      "description": "Try to check more than one option",
      "isRequired": false,
      "isVisible": true,
      "name": "chk_2",
      "questionNumber": "2",
      "title": "This is another checkbox"
    }
  ]
}
```

The result is a survey like the following screenshot:

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/de93706c-3403-4afb-ad81-3436a8f0ec3a)

 
#### Json Result

In debug and if the form is valid, the component shows the resulting `json`. Here an example:

```
{
  "chk_1": [
    {
      "value": 1,
      "text": "One"
    }
  ],
  "chk_2": [
    {
      "value": 1,
      "text": "One"
    }
  ]
}
```
