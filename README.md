# CSS-CODE-NOW
CSS CODE
<!DOCTYPE html>
<html>
  <head>
    <title>ACADEMIC INTEGRITY by ALEX CAVUILATI</title>
    <style>
      /* Define global styles */
      body {
        background-color: #000;
        color: #fff;
        font-family: Arial, sans-serif;
      }

      /* Style the header */
      h1 {
        color: #fff;
        text-align: center;
      }

      /* Style the form */
      form {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-top: 30px;
      }

      /* Style the form label */
      label {
        margin-top: 20px;
      }

      /* Style the file upload input */
      input[type="file"] {
        margin-top: 10px;
      }

      /* Style the submit button */
      button {
        margin-top: 20px;
        background-color: #0077c2;
        color: #fff;
        border: none;
        padding: 10px 20px;
        font-size: 18px;
        cursor: pointer;
      }

      /* Style the output container */
      #output {
        margin-top: 30px;
        border: 2px solid #0077c2;
        padding: 10px;
      }
    </style>
  </head>
  <body>
    <h1>ACADEMIC INTEGRITY</h1>
    <form>
      <label for="file-upload">Upload your file:</label>
      <input type="file" id="file-upload" accept=".txt">
      <button type="submit">Submit</button>
    </form>
    <div id="output"></div>

    <script>
      const chatGptCorpus = [
        "ChatGPT is a language model developed by OpenAI.",
        "It's designed to generate text based on patterns learned from large amounts of data.",
        "It can answer questions and generate text on a wide range of topics."
      ];

      function isChatGptText(inputText) {
        let similarity = 0;
        for (let i = 0; i < chatGptCorpus.length; i += 1) {
          const jaccardSimilarity = jaccard(inputText, chatGptCorpus[i]);
          similarity = Math.max(similarity, jaccardSimilarity);
        }
        return similarity >= 0.5;
      }

      function jaccard(str1, str2) {
        const set1 = new Set(str1.split(" "));
        const set2 = new Set(str2.split(" "));
        const intersection = new Set([...set1].filter(x => set2.has(x)));
        return intersection.size / (set1.size + set2.size - intersection.size);
      }

      const form = document.querySelector("form");
      const outputEl = document.getElementById("output");

      form.addEventListener("submit", (event) => {
        event.preventDefault();
        const fileInput = document.getElementById("file-upload");
        const file = fileInput.files[0];
        const reader = new FileReader();
        reader.readAsText(file);
        reader.onload = () => {
          outputEl.innerHTML = isChatGptText(reader.result);
        };
      });
    </script>
  </body>
</html>
