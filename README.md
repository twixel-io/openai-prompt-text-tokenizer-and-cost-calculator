# OpenAI Prompt Text Tokenizer & Cost Calculator API Tutorial

This tutorial will guide you on how to use the **OpenAI Prompt Text Tokenizer & Cost Calculator API** via [RapidAPI](https://bit.ly/openai-prompt-text-tokenizer-cost-calculator). This API is based on the Postman collection and will help you with tokenizing and calculating the cost of text prompts when using OpenAI's ChatGPT API.

By default, RapidAPI examples use Node.js and Axios, so this tutorial will provide samples using those. However, you can use many other programming languages and libraries, with samples available on RapidAPI.

Remember to join the [Discord community](https://discord.gg/E8G6azTQdn) for further assistance and discussions.

## Getting Started

1. Sign up or log in to [RapidAPI](https://rapidapi.com/).
2. Subscribe to the [OpenAI Prompt Text Tokenizer & Cost Calculator API](https://bit.ly/openai-prompt-text-tokenizer-cost-calculator).
3. Get your RapidAPI Key.

## API Endpoints

The API has three main endpoints:

1. Encode: Tokenize, get a token count and associated cost.
2. Decode: Convert tokenized string back to text.
3. Models: Retrieve available models and their associated token cost as per OpenAI's pricing page.

### 1. Encode: Tokenize, get a token count and associated cost

This endpoint allows you to tokenize a given text and get the number of tokens for that text. It also returns the associated cost for using the tokens with a specified model.

#### POST: `{{baseUrl}}/openai/chatgpt/encode`

**Request Headers**

```javascript
{
    "X-RapidAPI-Host": "openai-prompt-text-tokenizer-cost-calculator.p.rapidapi.com",
    "X-RapidAPI-Key": "Your RapidAPI Key Goes Here"
}
```

**Request Body (JSON)**

```json
{
    "model": "gpt-4",
    "inputType": "prompt",
    "text": "Your prompt text goes here!"
}
```

**Example with Node.js and Axios**

```javascript
const axios = require("axios");

const options = {
  method: "POST",
  url: "https://openai-prompt-text-tokenizer-cost-calculator.p.rapidapi.com/openai/chatgpt/encode",
  headers: {
    "X-RapidAPI-Host": "openai-prompt-text-tokenizer-cost-calculator.p.rapidapi.com",
    "X-RapidAPI-Key": "Your RapidAPI Key Goes Here",
    "Content-Type": "application/json"
  },
  data: {
    model: "gpt-4",
    inputType: "prompt",
    text: "Your prompt text goes here!"
  }
};

axios.request(options).then(response => {
  console.log(response.data);
}).catch(error => {
  console.error(error);
});
```

**Response (JSON)**

```json
{
    "model": "gpt-4",
    "inputType": "prompt",
    "tokens": 6,
    "costing": {
        "promptCostPer1KTokens": 0.03,
        "promptCostPerToken": 0.000029999999999999997,
        "completionCostPer1KToken": 0.06,
        "completionCostPerToken": 0.000059999999999999995,
        "totalCost": 0.00017999999999999998
    },
    "text": [
        7927,
        10137,
        1495,
        5900,
        1618,
        0
    ]
}
```

### 2. Decode: Convert tokenized string back to text

This endpoint helps you convert a tokenized string back into its original text form. It also returns the associated cost for the tokenized string.

#### POST: `{{baseUrl}}/openai/chatgpt/decode`

**Request Headers**

```javascript
{
    "X-RapidAPI-Host": "openai-prompt-text-tokenizer-cost-calculator.p.rapidapi.com",
    "X-RapidAPI-Key": "Your RapidAPI Key Goes Here"
}
```

**Request Body (JSON)**

```json
{
    "model": "gpt-4",
    "inputType": "prompt",
    "text": [
        7927,
        10137,
        1495,
        5900,
        1618,
        0
    ]
}
```

**Example with Node.js and Axios**

```javascript
const axios = require("axios");

const options = {
  method: "POST",
  url: "https://openai-prompt-text-tokenizer-cost-calculator.p.rapidapi.com/openai/chatgpt/decode",
  headers: {
    "X-RapidAPI-Host": "openai-prompt-text-tokenizer-cost-calculator.p.rapidapi.com",
    "X-RapidAPI-Key": "Your RapidAPI Key Goes Here",
    "Content-Type": "application/json"
  },
  data: {
    model: "gpt-4",
    inputType: "prompt",
    text: [7927, 10137, 1495, 5900, 1618, 0]
  }
};

axios.request(options).then(response => {
  console.log(response.data);
}).catch(error => {
  console.error(error);
});
```

**Response (JSON)**

```json
{
    "model": "gpt-4",
    "inputType": "prompt",
    "costing": {
        "promptCostPer1KTokens": 0.03,
        "promptCostPerToken": 0.000029999999999999997,
        "completionCostPer1KToken": 0.06,
        "completionCostPerToken": 0.000059999999999999995,
        "totalCost": 0.00081
    },
    "text": "Your prompt text goes here!"
}
```

### 3. Models: Retrieve available models and their associated token cost

This endpoint provides you with the list of available models and their pricing details.

#### GET: `{{baseUrl}}/openai/chatgpt/models`

**Request Headers**

```javascript
{
    "X-RapidAPI-Host": "openai-prompt-text-tokenizer-cost-calculator.p.rapidapi.com",
    "X-RapidAPI-Key": "Your RapidAPI Key Goes Here"
}
```

**Example with Node.js and Axios**

```javascript
const axios = require("axios");

const options = {
  method: "GET",
  url: "https://openai-prompt-text-tokenizer-cost-calculator.p.rapidapi.com/openai/chatgpt/models",
  headers: {
    "X-RapidAPI-Host": "openai-prompt-text-tokenizer-cost-calculator.p.rapidapi.com",
    "X-RapidAPI-Key": "Your RapidAPI Key Goes Here"
  }
};

axios.request(options).then(response => {
  console.log(response.data);
}).catch(error => {
  console.error(error);
});
```

**Response (JSON)**

The response will contain the available models and their pricing details.

```json
[
    {
        "model": "gpt-4",
        "promptCostPer1KTokens": 0.03,
        "promptCostPerToken": 0.000029999999999999997,
        "completionCostPer1KToken": 0.06,
        "completionCostPerToken": 0.000059999999999999995
    },
]
```

*Note:*

- Certain models have extremely big numbers for the **promptCostPerToken** fields, so far it's only applicable to the ADA related models. In this case, it's returned as a floating-point precision number in scientific notation or exponential notation.
- Models with 0 cost mean that there is no cost information available on OpenAI's website.


Here's a another example that includes three functions for each endpoint: `encodeText`, `decodeText`, and `getModels`. You can use these functions to easily interact with the OpenAI Prompt Text Tokenizer & Cost Calculator API.

First, install Axios:

```bash
npm install axios
```

Then, create a file called `openai_api.js` and add the following code:

```javascript
const axios = require("axios");

const rapidAPIKey = "Your RapidAPI Key Goes Here";
const baseUrl = "https://openai-prompt-text-tokenizer-cost-calculator.p.rapidapi.com";

const headers = {
  "X-RapidAPI-Host": "openai-prompt-text-tokenizer-cost-calculator.p.rapidapi.com",
  "X-RapidAPI-Key": rapidAPIKey,
  "Content-Type": "application/json",
};

async function encodeText(model, inputType, text) {
  const options = {
    method: "POST",
    url: `${baseUrl}/openai/chatgpt/encode`,
    headers: headers,
    data: {
      model,
      inputType,
      text,
    },
  };

  try {
    const response = await axios.request(options);
    return response.data;
  } catch (error) {
    console.error(error);
    return null;
  }
}

async function decodeText(data) {
  const options = {
    method: "POST",
    url: `${baseUrl}/openai/chatgpt/decode`,
    headers: headers,
    data: data,
  };

  try {
    const response = await axios.request(options);
    return response.data;
  } catch (error) {
    console.error(error);
    return null;
  }
}

async function getModels() {
  const options = {
    method: "GET",
    url: `${baseUrl}/openai/chatgpt/models`,
    headers: headers,
  };

  try {
    const response = await axios.request(options);
    return response.data;
  } catch (error) {
    console.error(error);
    return null;
  }
}

module.exports = {
  encodeText,
  decodeText,
  getModels,
};
```

Now you can use these functions in your main file (e.g., `index.js`):

```javascript
const openaiApi = require("./openai_api");

(async () => {
  const model = "gpt-4";
  const inputType = "prompt";
  const text = "Your prompt text goes here!";

  // Encode text
  const encodedData = await openaiApi.encodeText(model, inputType, text);
  console.log("Encoded Data:", encodedData);

  // Decode text
  const decodedText = await openaiApi.decodeText(encodedData);
  console.log("Decoded Text:", decodedText);

  // Get models
  const models = await openaiApi.getModels();
  console.log("Models:", models);
})();
```

You can now run the `index.js` file:

```bash
node index.js
```

This will output the results of encoding, decoding, and available models. Don't forget to replace `Your RapidAPI Key Goes Here` with your actual RapidAPI key.


That's it! Happy coding!