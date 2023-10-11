This example covers the use case showing end to end integration of WA with Watsonx.ai showing the value of customer care scenario enhanced via generative ai

### Step 1 - Download the json extension.

First we need to download the following json file https://github.com/watson-developer-cloud/assistant-toolkit/blob/master/integrations/extensions/starter-kits/language-model-watsonx/watsonx-openapi.json

### Step 2 - Create your Watson Assistant at IBM Cloud

Then we need to create our Watson Assistant.

https://www.ibm.com/products/watson-assistant/artificial-intelligence

After it is created we go to **Integrations**

![WACode1 ](./images/WACodeImage/WACode1.png)

then we go to **Extensions** and click Build custom extension

<img src="./images/WACodeImage/WACode2.png" width="20%" />

We click next and then we can name like WatsonX extension then next and we attach our wasonx-openapi.json

<img src="./images/WACodeImage/WACode3.png" width=50%>

then we have to add the **WatsonX** extension to Watson Assistant by click in Add

<img src="./images/WACodeImage/WACode4.png" width=50%>

you click Add

<img src="./images/WACodeImage/WACode5.png" width=50%>

During the setup of this extension, you require to get the API of the WatsonX.

### Step 3 - Create WatsonX account

To get his, first you need to go to your WatsonX account

https://www.ibm.com/watsonx

<img src="./images/WACodeImage/WACode5.png" width=50%>

### Step 4 - Create a prompt Lab

Then you can open the **Experiment** with the foundation models with **Prompt Lab**

Let us choose an simple example like **Marketing Generation**

<img src="./images/WACodeImage/WACode7.png" width=50%>

### Step 5 - Create personal API key

then under the view code we click create personal API key

<img src="./images/WACodeImage/WACode8.png" width=50%>

then we create our API key

<img src="./images/WACodeImage/WACode9.png" width=50%>

### Step 6- Setup WatsonX extension

then we copy it and we paste in our WatsonX extension

<img src="./images/WACodeImage/WACode10.png" width=50%>

then we save and finish

<img src="./images/WACodeImage/WACode11.png" width=50%>

### Step 7- Setup Watson Assistant with WatsonX

We return back to our Watson Assistant and we can create an action

<img src="./images/WACodeImage/WACode12.png" width=50%>

for example Marketing Generation

<img src="./images/WACodeImage/WACode13.png" width=50%>

We create the first step, we can say

**ADD**

and then we define a customer response like Free text

<img src="./images/WACodeImage/WACode14.png" width=50%>

then we create an extra step, the step we name

**Call watson extension**

and then we continue to next step by using an extension

<img src="./images/WACodeImage/WACode15.png" width=50%>

In order to setup the extension you requiere to go back to your WatsonX and see the code

in my example will have something like

```
curl "https://us-south.ml.cloud.ibm.com/ml/v1-beta/generation/text?version=2023-05-29" \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer YOUR_ACCESS_TOKEN' \
  -d $'{
  "model_id": "google/flan-t5-xxl",
  "input": "Generate a 5 sentence marketing message for a company with the given characteristics.\\n\\nDetails\\nCharacteristics:\\n\\nCompany - Golden Bank\\n\\nOffer includes - no fees, 2% interest rate, no minimum balance\\n\\nTone - informative\\n\\nResponse requested - click the link\\n\\nEnd date - July 15\\n\\nEmail\\n",
  "parameters": {
    "decoding_method": "sample",
    "max_new_tokens": 200,
    "min_new_tokens": 50,
    "random_seed": 111,
    "stop_sequences": [],
    "temperature": 0.8,
    "top_k": 50,
    "top_p": 1,
    "repetition_penalty": 2
  },
  "project_id": "MY_PROJECT_ID"
}'
```

we will use the previous information to setup our extension in Watson Assistant

    For the version you will use a text with 2023-05-29

    For input you will choose Action Step Variables and then you choose the first step 1.Please enter in your promt

<img src="./images/WACodeImage/WACode16.png" width=50%>


For model_id google/flan-t5-xxl

for project_id you paste your project id for example 4asdasdds-56ed-4eea-b36d you will have something like

<img src="./images/WACodeImage/WACode17.png" width=50%>

then for this example we will requiere additional options

<img src="./images/WACodeImage/WACode18.png" width=50%>

then click apply. Then we create a new step, with conditions,
we choose WatsonX extension(step2)

<img src="./images/WACodeImage/WACode19.png" width=50%>

then Ran successfully

<img src="./images/WACodeImage/WACode20.png" width=50%>

in order to express code we set variable values, and we create a New session variable

<img src="./images/WACodeImage/WACode21.png" width=50%>

we name result and will be free text and then apply.

<img src="./images/WACodeImage/WACode22.png" width=50%>

then we click set variable values and then expression

<img src="./images/WACodeImage/WACode23.png" width=50%>

then we type in the value of the variable

<img src="./images/WACodeImage/WACode24.png" width=50%>

and search action step variables

<img src="./images/WACodeImage/WACode25.png" width=50%>

and select 1.Please enter in your propmt. Then you add an space then ` + “ “$ and find WatsonX extension(step2)`

<img src="./images/WACodeImage/WACode26.png" width=50%>

then click on Body.results

<img src="./images/WACodeImage/WACode27.png" width=50%>

and you are going to have something like this

<img src="./images/WACodeImage/WACode28.png" width=50%>

due to you get an array, you add the following [0]["generated_text"] that together in my case in something like this

<img src="./images/WACodeImage/WACode29.png" width=50%>

then in the assitant says you add a function result

<img src="./images/WACodeImage/WACode30.png" width=50%>

and finally we click on preview.
