# breaktheschyme

## Description

This repository contains a script designed to help you quickly get answers to questions on web pages. It extracts visible question text and options from the page, sends them to a language model (Mistral), and displays the answer.

## Features

* **HotKey Activation:** Press `ALT+3` to trigger the script.
* **Question Extraction:** Automatically identifies and extracts question text and options from the current web page.
* **Answer Retrieval:** Sends the extracted question to the Mistral API to get an answer.
* **Temporary Display:** Displays the answer in a temporary overlay on the page.
* **Error Handling:** Displays an error message if the question can't be found or if there's an issue retrieving the answer.

**Important:** This script requires an API key for the Mistral API. You will need to obtain your own API key and replace the placeholder in the script.

## How to Use

1.  **Obtain a Mistral API Key:**
    * Go to the Mistral AI website.
    * Create an account or sign in.
    * Obtain your API key from your account settings.
2.  **Install a Userscript Manager:**
    * You'll need a browser extension like Tampermonkey (Chrome, Firefox, Safari) or Greasemonkey (Firefox).
3.  **Install the Script:**
    * Copy the code from `version.md`.
    * Open your userscript manager and create a new script.
    * Paste the code into the script editor.
    * **Replace the placeholder API key:** Find this line in the script:

        ```javascript
        const apiKey = atob("YOUR_API_KEY_HERE");  //Important: Replace with your API Key
        ```

        Replace `YOUR_API_KEY_HERE` with your actual AI(I used MISTRAL) API key.
    * Save the script.
4.  **Use the Script:**
    * Navigate to a web page containing the question you want to answer.
    * Press `ALT+3`.
    * The script will process the question and display the answer (or an error message) in a temporary overlay.

## Important Notes

* **API Key Security:** Your API key is sensitive. Do not share it publicly. It's best to keep this script only for your personal use.
* **Website Compatibility:** The script's ability to extract questions and options depends on the structure of the web page. It may not work correctly on all websites.
* **Cost:** Using the Mistral API may incur costs, depending on their pricing. Be aware of your usage and billing.
* **Error: "Could not retrieve an answer."**: This error can occur if the Mistral API key is invalid, the API is down, or the prompt was rejected. Check your API key and network connection.
* **Working Fine:** This script has been tested and is working fine as of the date of this README. However, website structures and API behaviors can change, so occasional updates may be necessary.

## Disclaimer

This script is provided as-is, for informational and personal use only. The author is not responsible for any issues that may arise from its use. Use this script responsibly and in accordance with the terms of service of the websites you use it on.
