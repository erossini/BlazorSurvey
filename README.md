# Survey components for Blazor

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/4cb8e86c-aaf8-4d17-bf56-203a42397e12)

This component is a survey generator for [Blazor WebAssembly](https://www.puresourcecode.com/tag/blazor-webassembly/) and [Blazor Server](https://www.puresourcecode.com/tag/blazor-server/). The component is built with .NET6 but it is working also with NET8.

> The source code is not publicly available. If you make a donation, please use the [Sponsor](https://github.com/sponsors/erossini) button at the top of the [GitHub repository](https://github.com/erossini/BlazorSurvey) and I will give you access to the NuGet feed. Alternatively, you can contact me on [PureSourceCode](http://www.puresourcecode.com/) for more info, licence and donation.

The source code of the demo project is not working if you don't have access to the private NuGet feed. You can check the demo [here](https://survey.puresourcecode.com).

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

A checkbox is a small interactive box that can be toggled by the user to indicate an affirmative or negative choice.
The user can select one or more than one choice in the list. If you want to allow the user to select only one choice for the list,
it is better to use the _Radiobutton_.
    
![image](https://github.com/erossini/BlazorSurvey/assets/9497415/12666728-a569-4bc7-958e-a6bed3b3a5ff)

```csharp
Form form = new Form()
{
    Elements = new List<IElement>()
    {
        new Checkbox()
        {
            Title = "This is a checkbox",
            Description = "Try to check more than one option",
            Choices = new List<object>()
            {
                "One",
                "Two",
                "Three",
                new CheckboxChoice()
                {
                    Label = "Four"
                }
            }
        },
        new Checkbox()
        {
            Title = "This is another checkbox",
            Description = "Try to check more than one option",
            Orientation = PSC.Survey.Shared.Enums.Orientation.Horizontal,
            Choices = new List<object>()
            {
                "One",
                "Two",
                "Three",
                new CheckboxChoice()
                {
                    Label = "Four"
                }
            }
        }
    }
};
```

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

A comment is a big _Textbox_ where the user can type any kind of text. Multilines are supported.

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/feae3ac0-e6d9-4343-9aa5-4e89e566eaff)

```csharp
Form form = new Form()
    {
        Elements = new List<IElement>()
        {
            new Comment()
            {
                Title = "This is a comment",
                Description = "Type everything you want to say"
            },
            new Comment()
            {
                Title = "Comment required",
                Description = "This comment must be have a value but max 50 characters",
                IsRequired = true,
                MaxLength = 50
            }
        }
    };
```

This is an example of the generated `json`:

```
{
  "cmt_1": "This is my first comment",
  "cmt_2": "This comment is required with a maximum of 50 char"
}
```

### Dropdown

A dropdown listis a graphical control element that allows the user to choose one or more value from a list.

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/293b54e9-0857-4345-813a-7892b088d165)

```csharp
Form form = new Form()
    {
        Elements = new List<IElement>()
        {
            new DropdownList()
            {
                Title = "This is a dropdown list",
                Choices = new List<object>()
                {
                    "First option",
                    new DropdownListChoice()
                    {
                            Value = "Second",
                            Label = "Second option"
                    },
                    "Third option"
                }
            },
            new DropdownList()
            {
                Title = "This is a dropdown list",
                IsMultiselect = true,
                Choices = new List<object>()
                {
                    "First option",
                    new DropdownListChoice()
                    {
                            Value = "Second",
                            Label = "Second option"
                    },
                    "Third option"
                }
            }
        }
    };
```

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

This component displays a HTML text and it is not related to a question. It can be used to display information in any part of the survey.

```csharp
Form form = new Form()
    {
        Elements = new List<IElement>()
        {
            new HTML()
            {
                Title = "This is a HTML component",
                Description = "Display HTML code",
                Body = "<h1>This is a title</h1><p>This is a paragraph</p>"
            }
        }
    };
```

### ImagePicker

This component displays a list of images and the user has to select one or more of them.

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/17d6dd7a-815f-4208-9860-bd956b2426aa)

```csharp
Form form = new Form()
    {
        Elements = new List<IElement>()
        {
            new ImagePicker()
            {
                Title = "This is an ImagePicker",
                Description = "Select one image from the following",
                Choices = new List<ImagePickerChoice>()
                {
                    new ImagePickerChoice() { ImageUrl = "http://placekitten.com/220/200", Text = "Kitten 1", Value = "1" },
                    new ImagePickerChoice() { ImageUrl = "http://placekitten.com/180/200", Text = "Kitten 2", Value = "2" },
                    new ImagePickerChoice() { ImageUrl = "http://placekitten.com/130/200", Text = "Kitten 3", Value = "3" },
                    new ImagePickerChoice() { ImageUrl = "http://placekitten.com/270/200", Text = "Kitten 4", Value = "4" }
                }
            },
            new ImagePicker()
            {
                Title = "Where do you like to live?",
                Description = "Select all the images you like from the following",
                IsMultiselect = true,
                Choices = new List<ImagePickerChoice>()
                {
                    new ImagePickerChoice() { ImageUrl = "https://www.w3schools.com/css/img_5terre.jpg", Text = "5 terre", Value = "1" },
                    new ImagePickerChoice() { ImageUrl = "https://www.w3schools.com/css/img_forest.jpg", Text = "Forest", Value = "2" },
                    new ImagePickerChoice() { ImageUrl = "https://www.w3schools.com/css/img_lights.jpg", Text = "Lights", Value = "3" },
                    new ImagePickerChoice() { ImageUrl = "https://www.w3schools.com/css/img_mountains.jpg", Text = "Mountains", Value = "4" },
                    new ImagePickerChoice() { ImageUrl = "https://www.w3schools.com/css/paris.jpg", Text = "Paris", Value = "5" }
                }
            }
        }
    };
```

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

A Likert scale is a close-ended, forced-choice scale used in a questionnaire that provides a series of answers that go from one extreme to another.

- A Likert scale enables respondents to choose from a linear set of responses that increase or decrease in intensity or strength. It is a close-ended, forced-choice scale.
- Widely used in psychological and other social science research today, Likert scales enable researchers to collect data that provides nuance and insight into participants’ opinions. This data is quantitative and can easily be analyzed statistically.
- Likert items often offer response categories on a 1-to-5 scale, but a range of options is possible, including 1-to-7 and 0-to-4 scales or even-numbered scales that typically range from 1-to-4 or 1-to-6.
    
![image](https://github.com/erossini/BlazorSurvey/assets/9497415/94e67e0d-c11e-4c29-9610-8ea6a2bfd3b0)

```csharp
Form form = new Form()
    {
        Elements = new List<IElement>()
        {
            new LikertSkill() { 
                Name = "lsk_1", Title = "Liker Skill Type 1", 
                LikertSkirtType = PSC.Survey.Shared.Enums.LikertSkillType.Agree 
            },
            new LikertSkill() { 
                Name = "lsk_2", Title = "Liker Skill Type 2", 
                LikertSkirtType = PSC.Survey.Shared.Enums.LikertSkillType.Helpful 
            },
            new LikertSkill() { 
                Name = "lsk_3", Title = "Liker Skill Type 3", 
                LikertSkirtType = PSC.Survey.Shared.Enums.LikertSkillType.Satisfied
            }
        }
    };
```

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

In a survey, a matrix question is a type of closed-ended question that offers respondents a selection of multiple answers to choose from within a single question. Unlike other closed-ended questions, a matrix question comprises a series of different questions that all share the same set of answer options.

The purpose of a matrix question is to efficiently gather information from respondents about a specific topic by providing them with a comprehensive range of answer options to choose from. This approach to questioning can help to reduce survey length and increase survey response rates, as respondents can quickly provide their answers to a series of related questions.

Overall, the use of matrix questions in surveys can be an effective way to gather detailed information from respondents in a streamlined and efficient manner.

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/2df09720-756a-40c1-8bf0-7138b7eb8771)

```csharp
Form form = new Form()
    {
        Elements = new List<IElement>()
        {
            new Matrix()
            {
                Title = "This is a matrix",
                Description = "Select the appropriate option",
                Columns = new List<string>()
                {
                    "Strongly agree", "Agree", "Neither agree or disagree", "Disagree", "Strongly disagree"
                },
                Rows = new List<string>()
                {
                    "I like to work", "I like staying at home", "I like to go on holidays" 
                }
            }
        }
    };
```

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

Net Promoter Score (NPS) is a customer loyalty and satisfaction measurement taken by asking customers how likely they are to recommend your product or service to others on a scale of 1-11 (or 0-10).

NPS can be used as a predictor of business growth. When your company’s NPS is high (or, at least, higher than the industry average), you know that you have a healthy relationship with customers who are likely to act as evangelists for the brand, fuel word of mouth, and generate a positive growth cycle.

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/06c6a9d1-4a65-4bb3-91f6-e16b8b278317)

```csharp
Form form = new Form()
    {
        Elements = new List<IElement>()
        {
            new NPS() { 
                Name = "nps1", 
                Title = "This is an example of NPS", 
                Description = "Select a value between 1 and 11" 
            }
        }
    };
```

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

The panel defines a group of elements that need to be highlighted.

```csharp
Form form = new Form()
    {
    Elements = new List<IElement>()
    {
        new Panel() {
            Name="pnl1",
            Title = "This is a panel",
            Description = "Panel example that conains other elements",
            PanelElements = new List<IElement>()
            {
                new Textbox() { Title = "Username", PlaceHolder = "Enter your new name", Name = "txtNewName",
                    Description = "Insert your new name", IsRequired = true },
                new Textbox() {
                    Title = "Password", PlaceHolder = "Enter your password", Name = "txtPassword", IsRequired = true,
                    TextboxType = PSC.Survey.Shared.Enums.TextboxType.Password
                },
                new LikertSkill() { Name = "lsk1", Title = "Liker Skill", LikertSkirtType = PSC.Survey.Shared.Enums.LikertSkillType.Agree }
            }
        },
        new Panel() {
            Name="pnl1",
            Title = "This is a second panel",
            Description = "Panel example that conains other elements",
            BackgroundColor = "#c0c0c0",
            PanelElements = new List<IElement>()
            {
                new Textbox() { Title = "Username", PlaceHolder = "Enter your new name", Name = "txtNewName",
                    Description = "Insert your new name", IsRequired = true },
                new Textbox() {
                    Title = "Password", PlaceHolder = "Enter your password", Name = "txtPassword", IsRequired = true,
                    TextboxType = PSC.Survey.Shared.Enums.TextboxType.Password
                }
            }
        }

    }
};
```

### Radiobutton

A radio button is one type of selection indicator in a list of options. If an option is selected, the circle is filled. If the option is not selected, the circle is empty.
When one circle is selected, the others are deselected, so that only one option may be selected at any time.

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/364076da-b596-4b2e-a444-6aba3c8b8be2)

```csharp
Form form = new Form()
    {
        Elements = new List<IElement>()
        {
            new Radiobutton() { Title = "This is a radiobutton", Description = "Select one of the following options",
                Name = "radio1", Choices = new List<object>() {
                    "One", "Two", "Three",
                    new RadiobuttonChoice() { Label = "Four" }
                }, IsRequired = true },
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
            new Radiobutton() { Title = "This is a second radiobutton", Description = "Select one of the following options",
                Name = "radio2", Choices = new List<object>() {
                    "21", "22", "23",
                    new RadiobuttonChoice() { Label = "24" }
                }, IsRequired = true, Orientation = PSC.Survey.Shared.Enums.Orientation.Horizontal },
            new Radiobutton() { Title = "This is a second radiobutton", Description = "Select one of the following options",
                Name = "radio3", Choices = new List<object>() {
                    "31", "32", "33",
                    new RadiobuttonChoice() { Label = "34" }
                }, 
                IsRequired = true,
                Orientation = PSC.Survey.Shared.Enums.Orientation.Horizontal,
                Theme = PSC.Survey.Shared.Enums.RadioTheme.Boxed }
            }
    };
```

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

A radio button is one type of selection indicator in a list of options. If an option is selected, the circle is filled. If the option is not selected, the circle is empty.
When one circle is selected, the others are deselected, so that only one option may be selected at any time.

A radio button is one type of selection indicator in a list of options. If an option is selected, the circle is filled. If the option is not selected, the circle is empty.
When one circle is selected, the others are deselected, so that only one option may be selected at any time.

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/b30db8b0-a98a-4fd0-9a3a-ae3f6430d764)

```csharp
Form form = new Form()
    {
        Elements = new List<IElement>()
        {
            new Rating() {
                Title = "How was your experience?",
                Description = "Select a value between 1 and 5"
            }
        }
    };
```

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

The slider can be used when allowing users to specify any numeric value within a preset range.
It is also known as the range slider because you are supposed to create a minimal and maximal value the user can choose from.

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/50fcfd7f-8312-4cfb-a00c-ce52183bb880)

```csharp
Form form = new Form()
    {
        Elements = new List<IElement>()
        {
            new Slider() {
                Name = "sld1",
                Title = "Slider",
                Description = "This is an example of a slider",
                MinValue = 1,
                MaxValue = 6,
                IsVisible = true,
                Choices = new List<SliderChoice>()
                {
                    new SliderChoice() { Value = 1, Label = "One" },
                    new SliderChoice() { Value = 3, Label = "Three" },
                    new SliderChoice() { Value = 6, Label = "Six" }
                },
                ShowAllTicks = true
            },
            new Slider() {
                Name = "sld2",
                Title = "Slider",
                Description = "This is an example of a slider",
                MinValue = 1,
                MaxValue = 11,
                IsVisible = true,
                Choices = new List<SliderChoice>()
                {
                    new SliderChoice() { Value = 1, Label = "One" },
                    new SliderChoice() { Value = 6, Label = "Six" },
                    new SliderChoice() { Value = 11, Label = "Eleven" }
                },
                ShowAllTicks = true
            },
        }
    };
```

This is an example of the generated `json`:

```
{
  "sld_1": 3
}
```

### Switch

The toggle switch represents a physical switch that allows users to turn things on or off, like a light switch. 
Use toggle switch controls to present users with two mutually exclusive options (such as on/off), 
where choosing an option provides immediate results.

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/ec348b5a-2c5b-458e-8b5a-54e58d46c055)

```csharp
Form form = new Form()
    {
        Elements = new List<IElement>()
        {
            new Switch()
            {
                Title = "This is a switch",
                Description = "The switch can be on or off"
            }
        }
    };
```

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

A text box is a rectangular area on the screen where you can enter text. 
It is a common user interface element found in many types of software programs, such as web browsers, email clients, and word processors. 
When you click in a text box, a flashing cursor is displayed, indicating you can begin typing. 
If you are using a tablet, tapping inside a text box may automatically display the on-screen keyboard.

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

### Show question number

If `ShowQuestionNumber` is set to `True`, the `Survey` shows the number of the question in progression.

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/e099a636-f8ac-4883-8784-f724625a1f24)

If it is set to `False`, only the title and the description are displayed.

![image](https://github.com/erossini/BlazorSurvey/assets/9497415/b787e655-ce0f-4246-a94c-cc26a3509f87)

Here an example.

```
<Survey Form="form" ShowQuestionNumber="false" />
```

### Show separator

The property `ShowSeparator` allows you to show or hide the separator between the elements of the form. By default, the separator is not visible. To show it, set to `True` the property `ShowSeparator`. For example:

```html
<Survey Form="form" ShowSeparator="true" 
```

The separator is a `div` with the `class` set to `separator`. You can customize the separator using the `css` file.

### SubmitButtonText

This is the text displayed on the button at the bottom of the survey to run the validation and generate the json. By default, the text of the button is `Submit`. To change the text, use the property `SubmitButtonText`. For example:

```
<Survey Form="form" SubmitButtonText="Send" />
```
