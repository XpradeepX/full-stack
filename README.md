# full-stack
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>API Frontend</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }
        .container {
            background-color: #ffffff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            max-width: 600px;
            width: 100%;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        textarea {
            width: calc(100% - 22px);
            height: 120px;
            margin: 10px 0;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 16px;
            resize: none;
        }
        button {
            display: block;
            width: 100%;
            padding: 10px;
            font-size: 16px;
            color: #fff;
            background-color: #007bff;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            margin: 10px 0;
        }
        button:hover {
            background-color: #0056b3;
        }
        select {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 16px;
            margin: 10px 0;
        }
        .section {
            margin-top: 20px;
        }
        .section h2 {
            color: #333;
        }
        .section p {
            font-size: 16px;
            color: #555;
        }
        @media (max-width: 600px) {
            textarea, button, select {
                font-size: 14px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>API Frontend</h1>
        <textarea id="jsonInput" placeholder='Enter JSON here...'></textarea>
        <button onclick="submitData()">Submit</button>
        
        <select id="sectionSelect" multiple>
            <option value="numbers">Numbers</option>
            <option value="characters">Characters</option>
            <option value="highestAlphabet">Highest Alphabet</option>
        </select>

        <div id="responseOutput" class="section"></div>
    </div>

    <script>
        const apiUrl = 'https://your-vercel-app.vercel.app/api/bfhl'; // Replace with your Vercel API URL

        async function submitData() {
            const jsonInput = document.getElementById('jsonInput').value;
            try {
                const response = await fetch(apiUrl, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: jsonInput,
                });
                const data = await response.json();
                displayResponse(data);
            } catch (error) {
                console.error('Error:', error);
            }
        }

        function displayResponse(data) {
            const sectionSelect = document.getElementById('sectionSelect');
            const selectedSections = Array.from(sectionSelect.selectedOptions).map(option => option.value);
            let output = '';

            if (selectedSections.includes('numbers')) {
                output += <h2>Numbers</h2><p>${data.numbers.join(', ') || 'None'}</p>;
            }
            if (selectedSections.includes('characters')) {
                output += <h2>Characters</h2><p>${data.alphabets.join(', ') || 'None'}</p>;
            }
            if (selectedSections.includes('highestAlphabet')) {
                output += <h2>Highest Alphabet</h2><p>${data.highest_alphabet.join(', ') || 'None'}</p>;
            }

            document.getElementById('responseOutput').innerHTML = output;
        }
    </script>
</body>
</html>
