# Add a Survey to a React Application

This step-by-step tutorial will help you get started with the SurveyJS Library in a React application. To add a survey to your React application, follow the steps below:

- [Install the `survey-react` npm Package](#install-the-survey-react-npm-package)
- [Configure Styles](#configure-styles)
- [Create a Model](#create-a-model)
- [Render the Survey](#render-the-survey)
- [Handle Survey Completion](#handle-survey-completion)

As a result, you will create a survey displayed below:

<iframe src="https://codesandbox.io/embed/musing-visvesvaraya-j206b?fontsize=14&hidenavigation=1&module=%2Fsrc%2FApp.js&theme=dark"
    style="width:100%; height:500px; border:0; border-radius: 4px; overflow:hidden;"
    title="SurveyJS - Add a Survey to a React Application"
    sandbox="allow-forms allow-modals allow-popups allow-presentation allow-same-origin allow-scripts"
></iframe>

You can find the full code in the following GitHub repository: <a href="https://github.com/surveyjs/code-examples/tree/main/get-started-react" target="_blank">Get Started with SurveyJS - React</a>.

## Install the `survey-react` npm Package

The SurveyJS Library for React is distributed as a <a href="https://www.npmjs.com/package/survey-react" target="_blank">survey-react</a> npm package. Run the following command to install it:

```cmd
npm install survey-react --save
```

## Configure Styles

SurveyJS is shipped with several style sheets that implement different themes. Import one of the style sheets in the React component in which your survey will be.

To apply the imported theme, call the `applyTheme(themeName)` method. Its argument accepts different values depending on the chosen theme:

- Modern theme      
*"modern"*

- Default theme (in various color schemes)     
*"default"*, *"orange"*, *"darkblue"*, *"darkrose"*, *"stone"*, *"winter"*, *"winterstone"*

- Bootstrap theme (if your application uses Bootstrap)       
*"bootstrap"*

For instance, the following code applies the Modern theme:

```js
// Modern theme
import 'survey-react/modern.min.css';
// Default theme
// import 'survey-react/survey.min.css';
import { StylesManager } from 'survey-react';

StylesManager.applyTheme("modern");
```

## Create a Model

A model describes the layout and contents of your survey. The simplest survey model contains one or several questions without layout modifications.

Models are specified by model definitions (JSON objects). For example, the following model definition declares two [textual questions](https://surveyjs.io/Documentation/Library?id=questiontextmodel), each with a [title](https://surveyjs.io/Documentation/Library?id=questiontextmodel#title) and a [name](https://surveyjs.io/Documentation/Library?id=questiontextmodel#name). Titles are displayed on screen. Names are used to identify the questions in code.

```js
const surveyJson = {
  questions: [{
    name: "FirstName",
    title: "Enter your first name:",
    type: "text"
  }, {
    name: "LastName",
    title: "Enter your last name:",
    type: "text"
  }]
};
```

To instantiate a model, pass the model definition to the [Model](https://surveyjs.io/Documentation/Library?id=surveymodel) constructor as shown in the code below. The model instance will be later used to render the survey.

```js
import { ..., Model } from 'survey-react';
// ...
function App() {
  const survey = new Model(surveyJson);

  return ... ;
}
```

<details>
    <summary>View full code</summary>  

```js
import 'survey-react/modern.min.css';
// import 'survey-react/survey.min.css';
import { StylesManager, Model } from 'survey-react';

StylesManager.applyTheme("modern");

const surveyJson = {
  questions: [{
    name: "FirstName",
    title: "Enter your first name:",
    type: "text"
  }, {
    name: "LastName",
    title: "Enter your last name:",
    type: "text"
  }]
};

function App() {
  const survey = new Model(surveyJson);

  return ...;
}

export default App;
```
</details>

## Render the Survey
To render a survey, import the `Survey` component, add it to the template, and pass the model instance you created in the previous step to the component's `model` attribute:

```js
import { ..., Survey } from 'survey-react';
// ...
const surveyJson = { ... };

function App() {
  const survey = new Model(surveyJson);

  return <Survey model={survey} />;
}
```

If you replicate the code correctly, you should see the following survey:

![Get Started with SurveyJS - Primitive Survey](images/get-started-primitive-survey.png)

<details>
    <summary>View full code</summary>  

```js
import 'survey-react/modern.min.css';
// import 'survey-react/survey.min.css';
import { Survey, StylesManager, Model } from 'survey-react';

StylesManager.applyTheme("modern");

const surveyJson = {
  questions: [{
    name: "FirstName",
    title: "Enter your first name:",
    type: "text"
  }, {
    name: "LastName",
    title: "Enter your last name:",
    type: "text"
  }]
};

function App() {
  const survey = new Model(surveyJson);

  return <Survey model={survey} />;
}

export default App;
```
</details>

## Handle Survey Completion

After a respondent completes a survey, the results are available within the [onComplete](https://surveyjs.io/Documentation/Library?id=surveymodel#onComplete) event handler. In real-world applications, you should send the results to a server where they will be stored in a database and processed. In this tutorial, the results are simply output in an alert dialog:

```js
import { useCallback } from 'react';
// ...
function App() {
  const survey = new Model(surveyJson);
  const alertResults = useCallback((sender) => {
    const results = JSON.stringify(sender.data);
    alert(results);
  }, []);

  survey.onComplete.add(alertResults);

  return <Survey model={survey} />;
}

```

![Get Started with SurveyJS - Survey Results](images/get-started-primitive-survey-alert.png)

As you can see, survey results are saved in a JSON object. Its properties correspond to the `name` property values of your questions in the model definition.


<details>
    <summary>View full code</summary>  

```js
import { useCallback } from 'react';

import 'survey-react/modern.min.css';
// import 'survey-react/survey.min.css';
import { Survey, StylesManager, Model } from 'survey-react';

StylesManager.applyTheme("modern");

const surveyJson = {
  questions: [{
    name: "FirstName",
    title: "Enter your first name:",
    type: "text"
  }, {
    name: "LastName",
    title: "Enter your last name:",
    type: "text"
  }]
};

function App() {
  const survey = new Model(surveyJson);
  const alertResults = useCallback((sender) => {
    const results = JSON.stringify(sender.data);
    alert(results);
  }, []);

  survey.onComplete.add(alertResults);

  return <Survey model={survey} />;
}

export default App;
```
</details>

## Conclusion

You have learnt how to add a survey to your React application. For further information, refer to help topics within the [Design a Survey](https://surveyjs.io/Documentation/Library?id=design-survey-create-a-simple-survey) section.