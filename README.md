<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Asistente Personal</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f0f2f5;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .chat-container {
            width: 400px;
            max-width: 90%;
            background: #fff;
            border-radius: 10px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }
        .chat-box {
            flex: 1;
            padding: 20px;
            overflow-y: auto;
        }
        .message {
            margin-bottom: 15px;
            padding: 10px 15px;
            border-radius: 20px;
            max-width: 75%;
            word-wrap: break-word;
        }
        .user {
            background: #007bff;
            color: white;
            align-self: flex-end;
        }
        .assistant {
            background: #e5e5ea;
            color: black;
            align-self: flex-start;
        }
        .input-box {
            display: flex;
            border-top: 1px solid #ccc;
        }
        input {
            flex: 1;
            padding: 15px;
            border: none;
            outline: none;
            font-size: 16px;
        }
        button {
            padding: 15px 20px;
            background: #007bff;
            border: none;
            color: white;
            cursor: pointer;
            font-size: 16px;
        }
    </style>
</head>
<body>

<div class="chat-container">
    <div class="chat-box" id="chatBox"></div>
    <div class="input-box">
        <input type="text" id="userInput" placeholder="Escribe tu pregunta...">
        <button onclick="sendMessage()">Enviar</button>
    </div>
</div>

<script>
    const chatBox = document.getElementById('chatBox');
    const userInput = document.getElementById('userInput');

    // Respuestas predefinidas simples
    const respuestas = {
        "hola": "¡Hola! ¿Cómo puedo ayudarte hoy?",
        "cómo estás": "Estoy bien, gracias por preguntar. ¿Y tú?",
        "qué puedes hacer": "Puedo responder preguntas simples y ayudarte con información básica.",
        "adiós": "¡Hasta luego! Que tengas un buen día."
    };

    function sendMessage() {
        const mensaje = userInput.value.trim();
        if (mensaje === "") return;

        // Mostrar mensaje del usuario
        appendMessage(mensaje, "user");
        userInput.value = "";

        // Generar respuesta del asistente
        setTimeout(() => {
            const respuesta = getRespuesta(mensaje.toLowerCase());
            appendMessage(respuesta, "assistant");
            chatBox.scrollTop = chatBox.scrollHeight;
        }, 500);
    }

    function appendMessage(text, sender) {
        const div = document.createElement('div');
        div.classList.add('message', sender);
        div.textContent = text;
        chatBox.appendChild(div);
    }

    function getRespuesta(input) {
        for (const key in respuestas) {
            if (input.includes(key)) {
                return respuestas[key];
            }
        }
        return "Lo siento, no entiendo tu pregunta.";
    }

    // Permitir enviar con Enter
    userInput.addEventListener('keypress', function(e) {
        if (e.key === 'Enter') sendMessage();
    });
</script>

</body>
</html>
