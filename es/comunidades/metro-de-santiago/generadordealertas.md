# Metro de Santiago Alert Generator

A quick interface to generate alert messages for Metro de Santiago stations.

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Generador de Alertas - Metro de Santiago</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background-color: #f5f5f5;
        }
        .container {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        h1 {
            color: #005baa;
            text-align: center;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        select, input, textarea {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            box-sizing: border-box;
        }
        textarea {
            height: 100px;
            resize: vertical;
        }
        button {
            background-color: #005baa;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #004080;
        }
        .alert-preview {
            margin-top: 20px;
            padding: 15px;
            background-color: #f8f9fa;
            border-left: 4px solid #005baa;
            white-space: pre-wrap;
            font-family: monospace;
        }
        .emoji-selector {
            display: flex;
            gap: 5px;
            margin-bottom: 10px;
        }
        .emoji-option {
            font-size: 20px;
            cursor: pointer;
            padding: 5px;
            border-radius: 4px;
        }
        .emoji-option:hover {
            background-color: #e9ecef;
        }
        .time-input {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .time-input input {
            width: 60px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Generador de Alertas Metro de Santiago</h1>
        
        <div class="form-group">
            <label>Tipo de Alerta</label>
            <select id="alert-type">
                <option value="delay">🐢 Demora/Frecuencia Irregular</option>
                <option value="failure">⚙️ Avería Técnica</option>
                <option value="emergency">⚠️ Emergencia/Freno de Emergencia</option>
                <option value="resolved">✅ Problema Resuelto</option>
                <option value="person">🚷 Persona en Vías</option>
                <option value="access">🛡️ Accesos Controlados</option>
                <option value="custom">Personalizado (seleccionar emoji)</option>
            </select>
        </div>

        <div class="form-group">
            <label>Emoji (para alertas personalizadas)</label>
            <div class="emoji-selector">
                <div class="emoji-option" onclick="selectEmoji('🐢')">🐢</div>
                <div class="emoji-option" onclick="selectEmoji('⚙️')">⚙️</div>
                <div class="emoji-option" onclick="selectEmoji('⚠️')">⚠️</div>
                <div class="emoji-option" onclick="selectEmoji('✅')">✅</div>
                <div class="emoji-option" onclick="selectEmoji('🚷')">🚷</div>
                <div class="emoji-option" onclick="selectEmoji('🛡️')">🛡️</div>
                <div class="emoji-option" onclick="selectEmoji('🔌')">🔌</div>
                <div class="emoji-option" onclick="selectEmoji('⌛')">⌛</div>
            </div>
            <input type="text" id="custom-emoji" placeholder="O escribe tu emoji aquí" style="display: none;">
        </div>

        <div class="form-group">
            <label>Línea(s) afectada(s)</label>
            <select id="line" multiple>
                <option value="1">Línea 1</option>
                <option value="2">Línea 2</option>
                <option value="3">Línea 3</option>
                <option value="4">Línea 4</option>
                <option value="4A">Línea 4A</option>
                <option value="5">Línea 5</option>
                <option value="6">Línea 6</option>
            </select>
        </div>

        <div class="form-group">
            <label>Estación (se cargará desde JSON)</label>
            <select id="station">
                <option value="">Seleccionar estación...</option>
                <!-- Stations will be loaded from JSON -->
            </select>
        </div>

        <div class="form-group">
            <label>Dirección del tren (opcional)</label>
            <select id="direction">
                <option value="">No especificar</option>
                <option value="San Pablo">San Pablo</option>
                <option value="Los Dominicos">Los Dominicos</option>
                <option value="La Cisterna">La Cisterna</option>
                <option value="Vespucio Norte">Vespucio Norte</option>
                <option value="Plaza de Maipú">Plaza de Maipú</option>
                <option value="Vicente Valdés">Vicente Valdés</option>
                <!-- More directions can be added -->
            </select>
        </div>

        <div class="form-group">
            <label>Hora del incidente</label>
            <div class="time-input">
                <input type="checkbox" id="include-time" checked>
                <input type="time" id="incident-time">
            </div>
        </div>

        <div class="form-group">
            <label>Detalles adicionales</label>
            <textarea id="details" placeholder="Ej: Entre 3 y 7 minutos de espera en los andenes..."></textarea>
        </div>

        <div class="form-group">
            <label>Notas adicionales (opcional, aparecerán con 📝)</label>
            <textarea id="notes" placeholder="Ej: esto empezó con freno de emergencia por procedimiento de salud..."></textarea>
        </div>

        <button onclick="generateAlert()">Generar Alerta</button>

        <div class="form-group">
            <label>Vista previa:</label>
            <div class="alert-preview" id="alert-preview"></div>
        </div>

        <button onclick="copyToClipboard()">Copiar al Portapapeles</button>
    </div>

    <script>
        // This will be replaced with actual station data from JSON
        function loadStations() {
            // TODO: Load stations from JSON file
            const stationSelect = document.getElementById('station');
            
            // Example - to be replaced with actual fetch from stations.json
            const exampleStations = [
                "Estación Central",
                "Santa Isabel",
                "San Pablo",
                "Estación del Sol",
                "Ñuble",
                "Plaza de Maipú",
                "Vicente Valdés",
                "Los Dominicos"
            ];
            
            exampleStations.forEach(station => {
                const option = document.createElement('option');
                option.value = station;
                option.textContent = station;
                stationSelect.appendChild(option);
            });
        }

        document.getElementById('alert-type').addEventListener('change', function() {
            const customEmojiField = document.getElementById('custom-emoji');
            if (this.value === 'custom') {
                customEmojiField.style.display = 'block';
            } else {
                customEmojiField.style.display = 'none';
            }
        });

        function selectEmoji(emoji) {
            document.getElementById('custom-emoji').value = emoji;
        }

        function generateAlert() {
            const alertType = document.getElementById('alert-type').value;
            const customEmoji = document.getElementById('custom-emoji').value;
            const lines = Array.from(document.getElementById('line').selectedOptions)
                .map(option => option.text);
            const station = document.getElementById('station').value;
            const direction = document.getElementById('direction').value;
            const includeTime = document.getElementById('include-time').checked;
            const time = document.getElementById('incident-time').value;
            const details = document.getElementById('details').value;
            const notes = document.getElementById('notes').value;

            let emoji;
            if (alertType === 'custom') {
                emoji = customEmoji || '⚠️';
            } else {
                const emojiMap = {
                    'delay': '🐢',
                    'failure': '⚙️',
                    'emergency': '⚠️',
                    'resolved': '✅',
                    'person': '🚷',
                    'access': '🛡️'
                };
                emoji = emojiMap[alertType] || '⚠️';
            }

            let alertText = emoji;
            
            // Add time if included
            if (includeTime && time) {
                const formattedTime = `[${time}]`;
                alertText += ` ${formattedTime}`;
            }
            
            // Add station if selected
            if (station) {
                alertText += ` ${station}`;
            }
            
            // Add direction if selected
            if (direction) {
                alertText += ` Dirección ${direction}`;
            }
            
            // Add lines if selected
            if (lines.length > 0) {
                alertText += ` en ${lines.join(', ')}`;
            }
            
            // Add details
            if (details) {
                alertText += `\n\n⌛ ${details}`;
            }
            
            // Add notes if provided
            if (notes) {
                alertText += `\n\n📝 ${notes}`;
            }

            document.getElementById('alert-preview').textContent = alertText;
        }

        function copyToClipboard() {
            const preview = document.getElementById('alert-preview');
            navigator.clipboard.writeText(preview.textContent)
                .then(() => alert('Alerta copiada al portapapeles!'))
                .catch(err => alert('Error al copiar: ' + err));
        }

        // Initialize
        window.onload = function() {
            loadStations();
            // Set current time as default
            const now = new Date();
            const hours = now.getHours().toString().padStart(2, '0');
            const minutes = now.getMinutes().toString().padStart(2, '0');
            document.getElementById('incident-time').value = `${hours}:${minutes}`;
        };
    </script>
</body>
</html>
