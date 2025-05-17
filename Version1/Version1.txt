(function() {
  async function getAnswer(content) {
    try {
      console.log("Processing question...");
      const formattedContent = `
Question: ${content.question}
${content.options.length > 0 ? 'Options:\n' + content.options.map((opt, i) => `${i + 1}. ${opt}`).join('\n') : ''}
\nPlease provide the correct answer with explanation.`;

      console.log("Sending content to Gemini:", formattedContent.substring(0, 100) + "...");

      const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent?key=AIzaSyBrhud2gyPEQ_J6fvjndQAluRW36JhfnFA, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ contents: [{ parts: [{ text: formattedContent }] }] })
      });

      const data = await response.json();

      if (data.candidates && data.candidates[0] && data.candidates[0].content) {
        const answer = data.candidates[0].content.parts[0].text;
        console.log("Answer:", answer);
        displayAnswer(answer);
      } else {
        displayError("Could not retrieve an answer.");
      }
    } catch (error) {
      console.error("Error getting answer:", error);
      displayError("An error occurred while getting the answer.");
    }
  }

  function extractVisibleText() {
    let questionText = '';
    const questionElements = Array.from(document.querySelectorAll('.question-text, .question-container, .questionText, h3, h4, p'));

    questionElements.forEach(el => {
      if (el.offsetParent !== null && (el.innerText || el.textContent).trim().length > 10) {
        questionText += (el.innerText || el.textContent).trim() + '\n';
      }
    });

    const options = [];
    const optionElements = Array.from(document.querySelectorAll('input[type="radio"], input[type="checkbox"]'));

    optionElements.forEach(el => {
      if (el.offsetParent !== null) {
        const label = el.labels && el.labels[0] ? (el.labels[0].innerText || el.labels[0].textContent) : document.querySelector(`label[for="${el.id}"]`)?.innerText;
        if (label) {
          options.push(label.trim());
        }
      }
    });

    return { question: questionText.trim(), options: options };
  }

  function displayAnswer(answer) {
    const answerDiv = createHiddenDiv(answer);
    document.body.appendChild(answerDiv);
    answerDiv.style.display = 'block';
    setTimeout(() => {
      answerDiv.style.display = 'none';
      answerDiv.remove();
    }, 2000); // 2 seconds
  }

  function displayError(message) {
    const errorDiv = createHiddenDiv(message);
    document.body.appendChild(errorDiv);
    errorDiv.style.display = 'block';
    setTimeout(() => {
      errorDiv.style.display = 'none';
      errorDiv.remove();
    }, 2000); // 2 seconds
  }

  function createHiddenDiv(text) {
    const div = document.createElement('div');
    div.style.position = 'fixed';
    div.style.top = '10px';
    div.style.left = '10px';
    div.style.background = 'rgba(0, 0, 0, 0.8)';
    div.style.color = 'white';
    div.style.padding = '10px';
    div.style.zIndex = '9999';
    div.style.display = 'none';
    div.textContent = text;
    return div;
  }

  async function processQuestion() {
    try {
      const content = extractVisibleText();
      if (!content.question) {
        console.log("Could not find any question text on this page.");
        displayError("Could not find any question text on this page.");
        return;
      }
      await getAnswer(content);
    } catch (error) {
      console.error("Error:", error);
      displayError("An error occurred while processing the question.");
    }
  }

  document.addEventListener('keydown', function(event) {
    if (event.altKey && event.key === '3') {
      console.log("ALT+3 hotkey detected, processing question...");
      processQuestion();
      event.preventDefault();
    }
  });

  console.log("AI assistant script loaded. Press ALT+3 to get answers.");
})();
