# Survey components for Blazor

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/4cb8e86c-aaf8-4d17-bf56-203a42397e12)

This component is a survey generator for [Blazor WebAssembly](https://www.puresourcecode.com/tag/blazor-webassembly/) and [Blazor Server](https://www.puresourcecode.com/tag/blazor-server/). The component is built with .NET6 but it is working also with NET8.

The source code is not publicly available, but you can check the demo [here](https://survey.puresourcecode.com).

If you are interested in using it or like to have the source code, please contact me.

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

## Components

Here is the description of all the elements in the `Survey` component.

### Checkbox

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/12666728-a569-4bc7-958e-a6bed3b3a5ff)

This is an example of the resulting `json`:

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
      "value": 2,
      "text": "Two"
    }
  ]
}
```

### Comment

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/feae3ac0-e6d9-4343-9aa5-4e89e566eaff)

This is an example of the generated `json`:

```
{
  "cmt_1": "This is my first comment",
  "cmt_2": "This comment is required with a maximum of 50 char"
}
```

### Dropdown

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/293b54e9-0857-4345-813a-7892b088d165)

This is an example of the generated `json`:

```
{
  "ddl_1": [
    {
      "value": "Second",
      "text": "Second option"
    }
  ],
  "ddl_2": [
    {
      "value": "3",
      "text": "Third option"
    }
  ]
}
```

### HTML

### ImagePicker

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/17d6dd7a-815f-4208-9860-bd956b2426aa)

This is an example of the generated `json`:

```
{
  "imp_1": [
    {
      "text": "Kitten 2",
      "value": "2"
    }
  ]
}
```

### LikertSkill

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/94e67e0d-c11e-4c29-9610-8ea6a2bfd3b0)

This is an example of the generated `json`:

```
{
  "lsk_1": {
    "value": 2,
    "text": "Agree"
  },
  "lsk_2": {
    "value": 3,
    "text": "Somewhat helpful"
  },
  "lsk_3": {
    "value": 4,
    "text": "Somewhat disatisfied"
  }
}
```

### Matrix

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/2df09720-756a-40c1-8bf0-7138b7eb8771)

This is an example of the resulting `json`:

```
{
  "mtx_1": [
    {
      "column": 2,
      "text": "Neither agree or disagree"
    },
    {
      "row": 1,
      "column": 1,
      "text": "Agree"
    },
    {
      "row": 2,
      "column": 4,
      "text": "Strongly disagree"
    }
  ]
}
```

### NPS

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/06c6a9d1-4a65-4bb3-91f6-e16b8b278317)

This is an example of the resulting `json`:

```
{
  "nps_1": {
    "value": 7,
    "text": "7"
  }
}
```

### Panel

### Radiobutton

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/364076da-b596-4b2e-a444-6aba3c8b8be2)

This is an example of the resulting `json`

```
{
  "radio1": {
    "value": 1,
    "text": "One"
  },
  "radio2": {
    "value": 2,
    "text": "22"
  },
  "radio3": {
    "value": 3,
    "text": "33"
  }
}
```

### Rating

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/b30db8b0-a98a-4fd0-9a3a-ae3f6430d764)

This is an example of the generated `json`:

```
{
  "rtn_1": {
    "value": 3,
    "text": "3"
  }
}
```

### Repeater

### Slider

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/50fcfd7f-8312-4cfb-a00c-ce52183bb880)

This is an example of the generated `json`:

```
{
  "sld_1": 3
}
```

### Switch

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/ec348b5a-2c5b-458e-8b5a-54e58d46c055)

This is an example of the generated `json`:

```
{
  "swc_1": [
    {
      "value": 1,
      "text": ""
    }
  ]
}
```

### TextBox

A `TextBox` is a place where the user can type some text like the following screenshot:

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/399cdf31-3934-4691-91d0-de51e91a5bb0)

The available types of `TextBox` are:

- Color
- Date
- DateTime
- Email
- Month
- Number
- Password
- Telephone
- Text
- Week
- URL

To create a `Survey` with all types, here a full example:

```
@if(form == null)
{
    <p>Generating form...</p>
}
else {
    <Survey Form="form" ShowDebug="true" OnFormValuesChanged="OnFormValuesChanges"
            OnFormSubmitted="OnFormSubmitted" OnFormSubmittedError="OnFormSubmittedError" />
}
```
and here the code

```csharp
@code {
    Form form;

    protected override async Task OnInitializedAsync()
    {
        form = new Form()
            {
                Elements = new List<IElement>()
                {
                    new Textbox() {
                        Title = "Normal textbox",
                        Description = "This is a normal textbox",
                        PlaceHolder = "Enter your name",
                        IsRequired = true },
                    new Textbox() {
                        Title = "Password",
                        PlaceHolder = "Enter your future password",
                        Name = "txtPassword",
                        TextboxType = PSC.Survey.Shared.Enums.TextboxType.Password,
                        IsRequired = true },
                    new Textbox() {
                        Title = "Textbox max length 10",
                        PlaceHolder = "Enter your name",
                        Name = "txtMaxLength",
                        MaxLength = 10,
                        IsRequired = true },
                    new Textbox() {
                        Title = "Email validation",
                        PlaceHolder = "Enter your email",
                        Name = "txtEmail",
                        TextboxType = PSC.Survey.Shared.Enums.TextboxType.Email },
                    new Textbox() {
                        Title = "Number validation",
                        PlaceHolder = "Enter a number",
                        Name = "txtNumber",
                        TextboxType = PSC.Survey.Shared.Enums.TextboxType.Number },
                    new Textbox() {
                        Title = "Your favorite color",
                        PlaceHolder = "Pick up a color",
                        Name = "txtColor",
                        TextboxType = PSC.Survey.Shared.Enums.TextboxType.Color },
                    new Textbox() {
                        Title = "Your favorite website",
                        PlaceHolder = "Enter the url",
                        Name = "txtUrl",
                        TextboxType = PSC.Survey.Shared.Enums.TextboxType.URL },
                    new Textbox() {
                        Title = "Phone number",
                        PlaceHolder = "Enter your phone number",
                        Name = "txtPhone",
                        TextboxType = PSC.Survey.Shared.Enums.TextboxType.Telephone },
                    new Textbox() {
                        Title = "Select a date",
                        PlaceHolder = "Pick up a date you like",
                        Name = "txtDate",
                        TextboxType = PSC.Survey.Shared.Enums.TextboxType.Date },
                    new Textbox() {
                        Title = "Select a date and time",
                        PlaceHolder = "Pick up a date you like",
                        Name = "txtDateTime",
                        TextboxType = PSC.Survey.Shared.Enums.TextboxType.DateTime },
                    new Textbox() {
                        Title = "Select a week",
                        PlaceHolder = "Pick up a week you like",
                        Name = "txtWeek",
                        TextboxType = PSC.Survey.Shared.Enums.TextboxType.Week },
                    new Textbox() {
                        Title = "Select a month",
                        PlaceHolder = "Pick up a month you like",
                        Name = "txtMonth",
                        TextboxType = PSC.Survey.Shared.Enums.TextboxType.Month },
                    new Panel()
                    {
                        Title = "This panel contains a Textbox",
                        PanelElements = new List<IElement>()
                        {
                            new Textbox() {
                                Title = "Normal textbox",
                                Description = "This is a normal textbox in a Panel",
                                PlaceHolder = "Enter your name"
                            }
                        }
                    }
                }
            };

        StateHasChanged();
    }

    private void OnFormValuesChanges()
    {
    }

    private async Task OnFormSubmitted(FormSubmittedEventArgs e)
    {
    }

    private async Task OnFormSubmittedError()
    {
    }
}
```

The result is the following screenshot:

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/05077b14-f72f-4829-8517-cc171c374783)

And this is the `json` that the `Survey` component generated when the user submits the form.

```
{
  "txt_1": "Enrico",
  "txt_2": "Password",
  "txt_3": "0123456789",
  "txt_4": "info@puresourcecode.com",
  "txt_5": "3",
  "txt_6": "#5c2828",
  "txt_7": "https://puresourcecode.com",
  "txt_8": "077",
  "txt_9": "2023-12-19",
  "txt_10": "2023-12-19T16:19:00",
  "txt_11": "2023-W51",
  "txt_12": "2023-12",
  "pnla346038ba8c34e0ab246bd0909e74984_txt_13.1": "Normal text"
}
```

## Events

Here is the explanation of all the events a `Survey` component can raise and how to use them.

### OnFormSubmitted



### OnFormSubmittedError

### OnFormValuesChanged

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

### SubmitButtonText

This is the text displayed on the button at the bottom of the survey to run the validation and generate the json. By default, the text of the button is `Submit`. To change the text, use the property `SubmitButtonText`. For example:

```
<Survey Form="form" SubmitButtonText="Send" />
```
