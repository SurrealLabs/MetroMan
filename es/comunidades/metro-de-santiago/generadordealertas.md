# Metro de Santiago Alert Generator v2

Now with comprehensive incident types and formatted outputs.

```html
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
            margin-right: 10px;
            margin-bottom: 10px;
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
            flex-wrap: wrap;
            gap: 5px;
            margin-bottom: 10px;
        }
        .emoji-option {
            font-size: 20px;
            cursor: pointer;
            padding: 5px;
            border-radius: 4px;
            background-color: #f0f0f0;
        }
        .emoji-option:hover {
            background-color: #e0e0e0;
        }
        .time-input {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .time-input input {
            width: 60px;
        }
        .procedure-buttons {
            display: flex;
            flex-wrap: wrap;
            gap: 5px;
            margin-bottom: 15px;
        }
        .procedure-btn {
            background-color: #e9ecef;
            color: #495057;
            border: 1px solid #ced4da;
        }
        .procedure-btn:hover {
            background-color: #d6d8db;
        }
        .direction-container {
            display: flex;
            gap: 10px;
        }
        .direction-container select {
            flex: 1;
        }
        .status-indicator {
            padding: 5px 10px;
            border-radius: 4px;
            font-weight: bold;
            display: inline-block;
            margin-right: 10px;
        }
        .status-normal {
            background-color: #d4edda;
            color: #155724;
        }
        .status-delayed {
            background-color: #fff3cd;
            color: #856404;
        }
        .status-suspended {
            background-color: #f8d7da;
            color: #721c24;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Generador de Alertas Metro de Santiago</h1>
        
        <div class="form-group">
            <label>Tipo de Incidente/Procedimiento</label>
            <div class="procedure-buttons">
                <button class="procedure-btn" onclick="setProcedure('person_on_tracks')">🚷 Persona en Vías</button>
                <button class="procedure-btn" onclick="setProcedure('severe_accident')">🚨 Accidente Grave</button>
                <button class="procedure-btn" onclick="setProcedure('emergency_brake')">⚠️ Frenazo de Emergencia</button>
                <button class="procedure-btn" onclick="setProcedure('train_failure')">⚙️ Avería de Tren</button>
                <button class="procedure-btn" onclick="setProcedure('door_failure')">⚙️ Avería de Puertas</button>
                <button class="procedure-btn" onclick="setProcedure('delays')">⏳ Atrasos</button>
                <button class="procedure-btn" onclick="setProcedure('power_outage')">🔌 Corte de Corriente</button>
                <button class="procedure-btn" onclick="setProcedure('health_incident')">🆘 Incidente de Salud</button>
                <button class="procedure-btn" onclick="setProcedure('express_route')">ℹ️ Ruta Expresa</button>
                <button class="procedure-btn" onclick="setProcedure('service_resumed')">✅ Servicio Reestablecido</button>
                <button class="procedure-btn" onclick="setProcedure('slow_service')">🐢 Servicio Lento</button>
                <button class="procedure-btn" onclick="setProcedure('controlled_access')">🛡️ Accesos Controlados</button>
                <button class="procedure-btn" onclick="setProcedure('custom')">Personalizado</button>
            </div>
        </div>

        <div class="form-group">
            <label>Emoji/Icono</label>
            <div class="emoji-selector">
                <div class="emoji-option" onclick="selectEmoji('🐢')">🐢</div>
                <div class="emoji-option" onclick="selectEmoji('⚙️')">⚙️</div>
                <div class="emoji-option" onclick="selectEmoji('⚠️')">⚠️</div>
                <div class="emoji-option" onclick="selectEmoji('✅')">✅</div>
                <div class="emoji-option" onclick="selectEmoji('🚷')">🚷</div>
                <div class="emoji-option" onclick="selectEmoji('🛡️')">🛡️</div>
                <div class="emoji-option" onclick="selectEmoji('🔌')">🔌</div>
                <div class="emoji-option" onclick="selectEmoji('⌛')">⌛</div>
                <div class="emoji-option" onclick="selectEmoji('⏳')">⏳</div>
                <div class="emoji-option" onclick="selectEmoji('🚨')">🚨</div>
                <div class="emoji-option" onclick="selectEmoji('ℹ️')">ℹ️</div>
                <div class="emoji-option" onclick="selectEmoji('🚄')">🚄</div>
                <div class="emoji-option" onclick="selectEmoji('👀')">👀</div>
                <div class="emoji-option" onclick="selectEmoji('⛔')">⛔</div>
                <div class="emoji-option" onclick="selectEmoji('🆘')">🆘</div>
                <div class="emoji-option" onclick="selectEmoji('🤷‍♂️')">🤷‍♂️</div>
            </div>
            <input type="text" id="custom-emoji" placeholder="O escribe tu emoji aquí">
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
            <label>Dirección del tren</label>
            <div class="direction-container">
                <select id="direction">
                    <option value="">No especificar</option>
                    <option value="San Pablo">San Pablo</option>
                    <option value="Los Dominicos">Los Dominicos</option>
                    <option value="La Cisterna">La Cisterna</option>
                    <option value="Vespucio Norte">Vespucio Norte</option>
                    <option value="Plaza de Maipú">Plaza de Maipú</option>
                    <option value="Vicente Valdés">Vicente Valdés</option>
                    <option value="Plaza Quilicura">Plaza Quilicura</option>
                    <option value="Fernando Castillo Velasco">Fernando Castillo Velasco</option>
                    <option value="Plaza de Puente Alto">Plaza de Puente Alto</option>
                </select>
                <select id="direction-type" style="width: 80px;">
                    <option value="">Normal</option>
                    <option value="⤵️">⤵️</option>
                    <option value="⤴️">⤴️</option>
                </select>
            </div>
        </div>

        <div class="form-group">
            <label>Hora del incidente</label>
            <div class="time-input">
                <input type="checkbox" id="include-time" checked>
                <input type="time" id="incident-time">
            </div>
        </div>

        <div class="form-group">
            <label>Detalles principales</label>
            <textarea id="details" placeholder="Ej: Tren continuó sin servicio..."></textarea>
        </div>

        <div class="form-group">
            <label>Notas adicionales (aparecerán con 👀)</label>
            <textarea id="notes" placeholder="Ej: Se estará retomando la frecuencia normal..."></textarea>
        </div>

        <div class="form-group">
            <label>Estado del servicio</label>
            <div>
                <span class="status-indicator status-normal" onclick="setServiceStatus('normal')">Normal</span>
                <span class="status-indicator status-delayed" onclick="setServiceStatus('delayed')">Con Demoras</span>
                <span class="status-indicator status-suspended" onclick="setServiceStatus('suspended')">Suspendido Parcial</span>
            </div>
            <div id="service-range" style="display: none; margin-top: 10px;">
                <label>Servicio disponible entre:</label>
                <div style="display: flex; gap: 10px;">
                    <select id="from-station" style="flex: 1;">
                        <option value="">Desde estación...</option>
                    </select>
                    <select id="to-station" style="flex: 1;">
                        <option value="">Hasta estación...</option>
                    </select>
                </div>
            </div>
        </div>

        <button onclick="generateAlert()">Generar Alerta</button>
        <button onclick="copyToClipboard()">Copiar al Portapapeles</button>

        <div class="form-group">
            <label>Vista previa:</label>
            <div class="alert-preview" id="alert-preview"></div>
        </div>
    </div>

    <script>
        // Current procedure type
        let currentProcedure = '';
        let currentServiceStatus = 'normal';
        
        // This will be replaced with actual station data from JSON
        async function loadStations() {
            try {
                // In a real implementation, this would fetch from stations.json
                // const response = await fetch('stations.json');
                // const data = await response.json();
                
                // For now we'll use a simplified version
                const exampleStations = [
                    "Estación Central", "Santa Isabel", "San Pablo", "Estación del Sol",
                    "Ñuble", "Plaza de Maipú", "Vicente Valdés", "Los Dominicos",
                    "Rodrigo de Araya", "Patronato", "Las Torres", "Baquedano",
                    "Los Héroes", "Blanqueado", "Salvador", "Hospital el Pino",
                    "Vespucio Norte", "Einstein", "Cal y Canto", "Plaza Quilicura"
                ];
                
                const stationSelect = document.getElementById('station');
                const fromStation = document.getElementById('from-station');
                const toStation = document.getElementById('to-station');
                
                exampleStations.forEach(station => {
                    const option = document.createElement('option');
                    option.value = station;
                    option.textContent = station;
                    stationSelect.appendChild(option.cloneNode(true));
                    fromStation.appendChild(option.cloneNode(true));
                    toStation.appendChild(option);
                });
            } catch (error) {
                console.error('Error loading stations:', error);
            }
        }

        function setProcedure(procedure) {
            currentProcedure = procedure;
            const emojiMap = {
                'person_on_tracks': '🚷',
                'severe_accident': '🚨',
                'emergency_brake': '⚠️',
                'train_failure': '⚙️',
                'door_failure': '⚙️',
                'delays': '⏳',
                'power_outage': '🔌',
                'health_incident': '🆘',
                'express_route': 'ℹ️',
                'service_resumed': '✅',
                'slow_service': '🐢',
                'controlled_access': '🛡️',
                'custom': ''
            };
            
            document.getElementById('custom-emoji').value = emojiMap[procedure] || '';
            
            // Set default messages for certain procedures
            const detailsMap = {
                'person_on_tracks': 'Persona que descendió a las vías',
                'severe_accident': 'Accidente grave en las vías',
                'emergency_brake': 'Procedimiento de freno de emergencia',
                'train_failure': 'Tren detenido bajo revisión técnica',
                'door_failure': 'Avería en puertas de tren',
                'power_outage': 'Corte de corriente momentáneo',
                'health_incident': 'Procedimiento de salud activado',
                'service_resumed': 'Servicio se ha restablecido',
                'slow_service': 'Operando con lentitud',
                'controlled_access': 'Accesos controlados en estación'
            };
            
            if (detailsMap[procedure]) {
                document.getElementById('details').value = detailsMap[procedure];
            }
            
            // Special handling for service status
            if (procedure === 'severe_accident') {
                setServiceStatus('suspended');
            } else if (['train_failure', 'door_failure', 'person_on_tracks'].includes(procedure)) {
                setServiceStatus('delayed');
            } else if (procedure === 'service_resumed') {
                setServiceStatus('normal');
            }
        }

        function setServiceStatus(status) {
            currentServiceStatus = status;
            const rangeDiv = document.getElementById('service-range');
            
            if (status === 'suspended') {
                rangeDiv.style.display = 'block';
            } else {
                rangeDiv.style.display = 'none';
            }
            
            // Update UI indicators
            document.querySelectorAll('.status-indicator').forEach(el => {
                el.style.backgroundColor = '';
                el.style.color = '';
            });
            
            if (status === 'normal') {
                document.querySelector('.status-normal').style.backgroundColor = '#d4edda';
                document.querySelector('.status-normal').style.color = '#155724';
            } else if (status === 'delayed') {
                document.querySelector('.status-delayed').style.backgroundColor = '#fff3cd';
                document.querySelector('.status-delayed').style.color = '#856404';
            } else if (status === 'suspended') {
                document.querySelector('.status-suspended').style.backgroundColor = '#f8d7da';
                document.querySelector('.status-suspended').style.color = '#721c24';
            }
        }

        function selectEmoji(emoji) {
            document.getElementById('custom-emoji').value = emoji;
        }

        function generateAlert() {
            const emoji = document.getElementById('custom-emoji').value;
            const lines = Array.from(document.getElementById('line').selectedOptions)
                .map(option => option.text);
            const station = document.getElementById('station').value;
            const direction = document.getElementById('direction').value;
            const directionType = document.getElementById('direction-type').value;
            const includeTime = document.getElementById('include-time').checked;
            const time = document.getElementById('incident-time').value;
            const details = document.getElementById('details').value;
            const notes = document.getElementById('notes').value;
            const fromStation = document.getElementById('from-station').value;
            const toStation = document.getElementById('to-station').value;

            let alertText = emoji || '⚠️';
            
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
                if (directionType) {
                    alertText += ` ${directionType} ${direction}`;
                } else {
                    alertText += ` Dirección ${direction}`;
                }
            }
            
            // Add lines if selected
            if (lines.length > 0) {
                alertText += ` en ${lines.join(', ')}`;
            }
            
            // Add details
            if (details) {
                alertText += `\n\n${emoji === 'ℹ️' ? 'ℹ️' : '⌛'} ${details}`;
            }
            
            // Add service status information
            if (currentServiceStatus === 'suspended' && fromStation && toStation) {
                alertText += `\n\n⛔ Servicio solo disponible entre:\n${fromStation} ↔ ${toStation}`;
            } else if (currentServiceStatus === 'delayed') {
                alertText += `\n\n⌛ Anticipar demoras y esperas mayores a la habitual`;
            }
            
            // Add notes if provided
            if (notes) {
                alertText += `\n\n👀 ${notes}`;
            }
            
            // Special handling for service resumed
            if (currentProcedure === 'service_resumed') {
                alertText += `\n\nℹ️ Recordar que esto no significa que estará todo bien, anticipar atrasos, demoras y saturación en andenes`;
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
            
            // Set default procedure
            setProcedure('custom');
        };
    </script>
</body>
</html>
