<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>RTO Report Generator Tool</title>
    <style>
        :root {
            --bg-color: #f0f2f5;
            --card-bg: #ffffff;
            --text-main: #1c1e21;
            --text-muted: #65676b;
            --border-color: #cbd5e1;
            --border-focus: #2563eb;
            --primary: #2563eb;
            --primary-hover: #1d4ed8;
            --viber-purple: #7360f2;
            --viber-hover: #5d48db;
            --accent-green: #10b981;
            --shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            --radius: 12px;
            --chat-bg: #e5ddd5;
            --chat-bubble: #ffffff;
            --chat-text: #111b21;
            --input-bg: #f8f9fa;
            --modal-bg: rgba(0, 0, 0, 0.6);
        }

        [data-theme="dark"] {
            --bg-color: #0f172a;
            --card-bg: #1e293b;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border-color: #334155;
            --border-focus: #60a5fa;
            --primary: #3b82f6;
            --primary-hover: #2563eb;
            --viber-purple: #7360f2;
            --viber-hover: #5d48db;
            --accent-green: #10b981;
            --shadow: 0 4px 16px rgba(0, 0, 0, 0.4);
            --chat-bg: #0f172a;
            --chat-bubble: #1e293b;
            --chat-text: #f1f5f9;
            --input-bg: #0f172a;
            --modal-bg: rgba(0, 0, 0, 0.8);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            padding: 12px;
            padding-bottom: 50px;
            max-width: 520px;
            margin: 0 auto;
            transition: background-color 0.3s ease, color 0.3s ease;
        }

        .header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 14px;
            padding: 6px 0;
        }

        .header-title h1 {
            font-size: 1.25rem;
            font-weight: 800;
            color: var(--text-main);
            letter-spacing: -0.3px;
        }

        .header-title p {
            font-size: 0.75rem;
            color: var(--text-muted);
            margin-top: 2px;
        }

        .header-actions {
            display: flex;
            gap: 8px;
        }

        .icon-btn {
            background: var(--card-bg);
            border: 1px solid var(--border-color);
            color: var(--text-main);
            padding: 8px 12px;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 5px;
            box-shadow: var(--shadow);
            transition: all 0.2s ease;
        }

        .icon-btn:active {
            transform: scale(0.95);
        }

        .card {
            background: var(--card-bg);
            border-radius: var(--radius);
            padding: 16px;
            box-shadow: var(--shadow);
            margin-bottom: 14px;
            border: 1px solid var(--border-color);
            transition: background-color 0.3s ease, border-color 0.3s ease;
        }

        .form-group {
            margin-bottom: 12px;
        }

        .form-group:last-child {
            margin-bottom: 0;
        }

        label {
            display: block;
            font-size: 0.75rem;
            font-weight: 700;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            color: var(--text-muted);
            margin-bottom: 6px;
        }

        label.required::after {
            content: " *";
            color: #ef4444;
        }

        select, input, textarea {
            width: 100%;
            padding: 10px 12px;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            font-size: 0.9rem;
            background-color: var(--input-bg);
            color: var(--text-main);
            outline: none;
            transition: border-color 0.2s, background-color 0.2s;
        }

        select:focus, input:focus, textarea:focus {
            border-color: var(--border-focus);
            background-color: var(--card-bg);
        }

        select {
            appearance: none;
            background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%3c3b82f6' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6 9 12 15 18 9'%3e%3c/polyline%3e%3c/svg%3e");
            background-repeat: no-repeat;
            background-position: right 12px center;
            background-size: 16px;
            font-weight: 600;
            color: var(--border-focus);
        }

        textarea {
            resize: vertical;
            min-height: 70px;
        }

        .bullet-row {
            display: flex;
            align-items: center;
            gap: 6px;
            margin-bottom: 8px;
        }

        .bullet-row.indent-1 {
            padding-left: 20px;
        }

        .bullet-row input {
            flex: 1;
        }

        .bullet-row-btn {
            background: rgba(239, 68, 68, 0.1);
            color: #ef4444;
            border: 1px solid rgba(239, 68, 68, 0.2);
            padding: 8px 10px;
            border-radius: 6px;
            font-size: 0.8rem;
            font-weight: bold;
            cursor: pointer;
        }

        .manual-tools {
            display: flex;
            gap: 8px;
            margin-top: 8px;
        }

        .btn-sm {
            padding: 8px 12px;
            font-size: 0.8rem;
            border-radius: 6px;
            border: 1px solid var(--border-color);
            background: var(--input-bg);
            color: var(--text-main);
            font-weight: 600;
            cursor: pointer;
        }

        .btn-group {
            display: flex;
            flex-direction: column;
            gap: 10px;
            margin-top: 14px;
        }

        .btn {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
            width: 100%;
            padding: 12px;
            border: none;
            border-radius: 8px;
            font-size: 0.9rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.2s ease;
            position: relative;
        }

        .btn:active {
            transform: scale(0.98);
        }

        .btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none !important;
        }

        .btn-viber {
            background-color: var(--viber-purple);
            color: #ffffff;
        }

        .btn-viber:hover:not(:disabled) {
            background-color: var(--viber-hover);
        }

        .btn-secondary {
            background-color: var(--input-bg);
            color: var(--text-main);
            border: 1px solid var(--border-color);
        }

        .btn-excel {
            background-color: var(--accent-green);
            color: #ffffff;
        }

        .preview-container {
            position: relative;
            background: var(--chat-bg);
            border-radius: var(--radius);
            padding: 12px;
            margin-top: 6px;
            border: 1px solid var(--border-color);
        }

        .chat-bubble {
            background: var(--chat-bubble);
            border-radius: 8px 8px 8px 0px;
            padding: 12px;
            box-shadow: 0 1px 2px rgba(0,0,0,0.15);
            position: relative;
            font-family: -apple-system, Roboto, sans-serif;
            white-space: pre-wrap;
            word-wrap: break-word;
            font-size: 0.88rem;
            line-height: 1.45;
            color: var(--chat-text);
        }

        .toast {
            position: fixed;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%) translateY(100px);
            background: #0f172a;
            color: #ffffff;
            border: 1px solid #334155;
            padding: 12px 20px;
            border-radius: 25px;
            font-size: 0.85rem;
            font-weight: 600;
            box-shadow: 0 4px 16px rgba(0,0,0,0.3);
            transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            z-index: 2000;
            pointer-events: none;
        }

        .toast.show {
            transform: translateX(-50%) translateY(0);
        }

        .error-border {
            border-color: #ef4444 !important;
            background-color: rgba(239, 68, 68, 0.1) !important;
        }

        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            background: var(--modal-bg);
            backdrop-filter: blur(4px);
            z-index: 1500;
            display: none;
            justify-content: center;
            align-items: flex-end;
        }

        .modal-overlay.active {
            display: flex;
        }

        .modal-content {
            background: var(--card-bg);
            width: 100%;
            max-width: 520px;
            max-height: 85vh;
            border-radius: 20px 20px 0 0;
            padding: 18px;
            display: flex;
            flex-direction: column;
            box-shadow: var(--shadow);
            animation: slideUp 0.3s ease-out;
            border-top: 1px solid var(--border-color);
        }

        @keyframes slideUp {
            from { transform: translateY(100%); }
            to { transform: translateY(0); }
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
            padding-bottom: 8px;
            border-bottom: 1px solid var(--border-color);
        }

        .modal-header h2 {
            font-size: 1.1rem;
            font-weight: 700;
        }

        .modal-close {
            background: none;
            border: none;
            font-size: 1.4rem;
            color: var(--text-muted);
            cursor: pointer;
        }

        .history-controls {
            display: flex;
            flex-direction: column;
            gap: 8px;
            margin-bottom: 12px;
        }

        .history-filters {
            display: flex;
            gap: 8px;
        }

        .history-list {
            overflow-y: auto;
            flex: 1;
            display: flex;
            flex-direction: column;
            gap: 10px;
            padding-right: 4px;
        }

        .history-card {
            background: var(--input-bg);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 12px;
            position: relative;
        }

        .history-card-header {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 6px;
        }

        .history-type {
            font-size: 0.75rem;
            font-weight: 700;
            color: var(--primary);
            text-transform: uppercase;
        }

        .history-date {
            font-size: 0.7rem;
            color: var(--text-muted);
        }

        .history-body {
            font-size: 0.8rem;
            color: var(--text-main);
            white-space: pre-wrap;
            max-height: 80px;
            overflow: hidden;
            text-overflow: ellipsis;
            margin-bottom: 8px;
            line-height: 1.35;
        }

        .history-actions {
            display: flex;
            justify-content: flex-end;
            gap: 8px;
        }

        .badge-count {
            background: #ef4444;
            color: white;
            font-size: 0.65rem;
            padding: 2px 6px;
            border-radius: 10px;
            font-weight: bold;
        }

        /* CONFIRMATION POPUP MODAL */
        .confirm-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            background: rgba(0, 0, 0, 0.65);
            backdrop-filter: blur(5px);
            z-index: 3000;
            display: none;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .confirm-overlay.active {
            display: flex;
        }

        .confirm-card {
            background: var(--card-bg);
            border: 1px solid var(--border-color);
            border-radius: 16px;
            padding: 24px 20px;
            width: 100%;
            max-width: 380px;
            text-align: center;
            box-shadow: 0 10px 25px rgba(0,0,0,0.3);
            animation: popIn 0.25s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }

        @keyframes popIn {
            from { transform: scale(0.8); opacity: 0; }
            to { transform: scale(1); opacity: 1; }
        }

        .check-circle {
            width: 60px;
            height: 60px;
            background: rgba(16, 185, 129, 0.15);
            color: var(--accent-green);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 14px auto;
        }

        .confirm-card h3 {
            font-size: 1.15rem;
            font-weight: 800;
            color: var(--text-main);
            margin-bottom: 6px;
        }

        .confirm-card p {
            font-size: 0.85rem;
            color: var(--text-muted);
            line-height: 1.4;
            margin-bottom: 18px;
        }

        .confirm-card .btn-ok {
            background: var(--primary);
            color: #ffffff;
            padding: 10px 24px;
            border-radius: 8px;
            font-weight: 700;
            font-size: 0.9rem;
            border: none;
            cursor: pointer;
            width: 100%;
        }
    </style>
</head>
<body>

    <div class="header">
        <div class="header-title">
            <h1>RTO Report Generator Tool</h1>
            <p>Operations Notice Tool & Repository</p>
        </div>
        <div class="header-actions">
            <button class="icon-btn" onclick="openHistoryModal()">
                <span>📜 Log</span>
                <span class="badge-count" id="historyBadge">0</span>
            </button>
            <button class="icon-btn" id="themeToggleBtn" onclick="toggleTheme()">
                <span id="themeIcon">🌙</span>
            </button>
        </div>
    </div>

    <!-- Notice Type Selector Card -->
    <div class="card">
        <div class="form-group">
            <label for="noticeType">Select Report / Notice Type</label>
            <select id="noticeType" onchange="renderFormFields()">
                <option value="contingency_removal">Contingency List Removal Notice</option>
                <option value="hvdc_limit">HVDC Limit Change Update</option>
                <option value="market_intervention">Market Intervention Notice</option>
                <option value="lifting_market_intervention">Lifting of Market Intervention Notice</option>
                <option value="contingency_congestion">Contingency Congestion Notice</option>
                <option value="base_case_congestion">Base Case Congestion Notice</option>
                <option value="load_curtailment">Regional Load Curtailment Notice</option>
                <option value="manual_notice">Manual Input Notice / Freeform Advisory</option>
            </select>
        </div>
    </div>

    <!-- Dynamic Form Container -->
    <div class="card" id="formFields"></div>

    <!-- Dispatcher Signature Card -->
    <div class="card">
        <div class="form-group">
            <label for="reporterName" class="required">Dispatcher / Reporter Name</label>
            <input type="text" id="reporterName" placeholder="e.g. Gian Salle" oninput="saveReporterInfo(); updatePreview();">
        </div>
        <div class="form-group">
            <label for="reporterRole">Role / Shift (Optional)</label>
            <input type="text" id="reporterRole" placeholder="e.g. RTO-Visayas / Duty Dispatcher" oninput="saveReporterInfo(); updatePreview();">
        </div>
    </div>

    <!-- Live Preview & Action Buttons -->
    <div class="card">
        <label>Live Operational Preview</label>
        <div class="preview-container">
            <div class="chat-bubble" id="previewText">Fill in form fields above to view preview...</div>
        </div>
        
        <div class="btn-group">
            <button class="btn btn-secondary" id="btnCopyOnly" onclick="copyTextOnly()">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="9" y="9" width="13" height="13" rx="2" ry="2"></rect><path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"></path></svg>
                <span id="btnCopyOnlyText">Copy Report Text</span>
            </button>
            <button class="btn btn-viber" id="btnCopyViber" onclick="copyAndRedirectViber()">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M19.37 16.03c-.52-.35-2.92-1.44-3.37-1.61-.45-.16-.78-.24-1.11.25-.33.49-1.28 1.61-1.57 1.94-.29.33-.58.37-1.1.11-.52-.26-2.19-.81-4.18-2.58-1.55-1.38-2.6-3.09-2.9-3.61-.3-.52-.03-.8.23-1.06.23-.23.52-.61.78-.91.26-.3.35-.52.52-.87.17-.35.09-.65-.04-.91-.13-.26-1.11-2.68-1.52-3.67-.4-.96-.82-.83-1.12-.85-.29-.02-.63-.02-.97-.02-.35 0-.91.13-1.38.65-.47.52-1.8 1.76-1.8 4.29 0 2.53 1.84 4.97 2.1 5.32.26.35 3.62 5.53 8.78 7.75 1.23.53 2.19.85 2.94 1.09 1.23.39 2.35.33 3.23.2 1-.15 3.07-1.25 3.5-2.46.43-1.21.43-2.25.3-2.47-.12-.22-.43-.35-.95-.61z"/></svg>
                <span id="btnCopyViberText">Copy & Open Viber</span>
            </button>
        </div>
    </div>

    <!-- History Drawer Modal -->
    <div class="modal-overlay" id="historyModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Operational Report Repository</h2>
                <button class="modal-close" onclick="closeHistoryModal()">&times;</button>
            </div>
            <div class="history-controls">
                <input type="text" id="historySearch" placeholder="Search keyword..." oninput="renderHistoryList()">
                <div class="history-filters">
                    <select id="historyFilterType" onchange="renderHistoryList()">
                        <option value="ALL">All Notice Types</option>
                        <option value="contingency_removal">Contingency Removal</option>
                        <option value="hvdc_limit">HVDC Limit</option>
                        <option value="market_intervention">Market Intervention</option>
                        <option value="lifting_market_intervention">Lifting Market Intervention</option>
                        <option value="contingency_congestion">Contingency Congestion</option>
                        <option value="base_case_congestion">Base Case Congestion</option>
                        <option value="load_curtailment">Load Curtailment</option>
                        <option value="manual_notice">Manual Notice</option>
                    </select>
                    <select id="historySort" onchange="renderHistoryList()">
                        <option value="NEWEST">Newest First</option>
                        <option value="OLDEST">Oldest First</option>
                    </select>
                </div>
            </div>

            <div class="history-list" id="historyListContainer"></div>

            <div style="margin-top: 12px; display: flex; gap: 8px;">
                <button class="btn btn-excel" onclick="exportToGoogleSheetsCSV()">
                    📊 Export CSV
                </button>
                <button class="btn btn-secondary" onclick="clearAllHistory()" style="width: auto; padding: 0 12px; color: #ef4444; border-color: rgba(239, 68, 68, 0.3);">
                    🗑️ Clear
                </button>
            </div>
        </div>
    </div>

    <!-- Animated Confirmation Modal -->
    <div class="confirm-overlay" id="confirmOverlay">
        <div class="confirm-card">
            <div class="check-circle">
                <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><polyline points="20 6 9 17 4 12"></polyline></svg>
            </div>
            <h3 id="confirmTitle">Report Text Copied!</h3>
            <p id="confirmSubtitle">The formatted notice has been saved to clipboard and synced to Google Sheets.</p>
            <button class="btn-ok" onclick="closeConfirmModal()">OK</button>
        </div>
    </div>

    <div class="toast" id="toast">Copied to clipboard!</div>

    <script>
        // HARDCODED GOOGLE APPS SCRIPT WEB APP ENDPOINT
        const GOOGLE_SCRIPT_WEB_APP_URL = "https://script.google.com/macros/s/AKfycbzg667S28kP8RWTpGBHb4vu2DPLwOJe5_gzOzv8o1931i6fku0eSDSVZtN0lWnKBJdH6A/exec";

        const schemas = {
            contingency_removal: {
                title: 'Contingency List Removal Notice',
                fields: [
                    { id: 'marketRun', label: 'Market Run', placeholder: 'e.g. RTD' },
                    { id: 'effective', label: 'Effective Time', placeholder: 'e.g. 1655H RTD' },
                    { id: 'contingencyEquipment', label: 'Contingency Equipment', placeholder: 'e.g. 1SJO_1MRL1' },
                    { id: 'outageRelated', label: 'Outage Related', placeholder: 'e.g. 3TAY_3TWP1' },
                    { id: 'outageDate', label: 'Outage Date & Time', placeholder: 'e.g. 09/27/26 0300H - 1700H' },
                    { id: 'actualOnline', label: 'Actual Online Details', type: 'textarea', placeholder: 'e.g. Tayabas - Tanay Wind Power 500kV Line restored at 1637H.' }
                ]
            },
            hvdc_limit: {
                title: 'HVDC Limit Change Update',
                fields: [
                    { id: 'event', label: 'Event', placeholder: 'e.g. Luz-Vis HVDC Limit Adjustment' },
                    { id: 'parameter', label: 'Parameter', placeholder: 'e.g. HVDC Reverse Limit' },
                    { id: 'previousLimit', label: 'Previous Limit', placeholder: 'e.g. 50MW' },
                    { id: 'newLimit', label: 'New Limit', placeholder: 'e.g. 120MW' },
                    { id: 'date', label: 'Date', placeholder: 'e.g. 09/27/2026' },
                    { id: 'effective', label: 'Effective Time', placeholder: 'e.g. 1710H RTD' }
                ]
            },
            market_intervention: {
                title: 'Market Intervention Notice',
                fields: [
                    { id: 'region', label: 'Region', placeholder: 'e.g. Visayas' },
                    { id: 'event', label: 'Event', placeholder: 'e.g. System Operator (SO) Initiated Market Intervention' },
                    { id: 'date', label: 'Date', placeholder: 'e.g. 09/23/2026' },
                    { id: 'start', label: 'Start Time', placeholder: 'e.g. 1515H-ongoing' },
                    { id: 'cause', label: 'Cause', type: 'textarea', placeholder: 'e.g. Implementation of Manual Load Dropping (MLD)...' },
                    { id: 'marketImpact', label: 'Market Impact', type: 'textarea', placeholder: 'e.g. Administered Pricing (AP) applied to Visayas.' },
                    { id: 'actionTaken', label: 'Action Taken', type: 'textarea', placeholder: 'e.g. AP Flag activated in COP reflected starting 1525H.' }
                ]
            },
            lifting_market_intervention: {
                title: 'Lifting of Market Intervention Notice',
                fields: [
                    { id: 'region', label: 'Region', placeholder: 'e.g. Visayas' },
                    { id: 'event', label: 'Event', placeholder: 'e.g. System Operator (SO) Initiated Market Intervention' },
                    { id: 'date', label: 'Date', placeholder: 'e.g. 09/23/2026' },
                    { id: 'start', label: 'Start Time', placeholder: 'e.g. 1515H-2155H' },
                    { id: 'duration', label: 'Duration', placeholder: 'e.g. 6hrs and 45mins' },
                    { id: 'cause', label: 'Cause', type: 'textarea', placeholder: 'e.g. Implementation of Manual Load Dropping (MLD)...' },
                    { id: 'marketImpact', label: 'Market Impact', type: 'textarea', placeholder: 'e.g. Administered Pricing (AP) applied to Visayas.' },
                    { id: 'actionTaken', label: 'Action Taken', type: 'textarea', placeholder: 'e.g. AP Flag deleted in COP starting 2155H in DIPC run.' }
                ]
            },
            contingency_congestion: {
                title: 'Contingency Congestion Notice',
                fields: [
                    { id: 'elementHeader', label: 'Header Element Identifier', placeholder: 'e.g. 3DASMA_TR1' },
                    { id: 'marketRun', label: 'Market Run', placeholder: 'e.g. RTD' },
                    { id: 'region', label: 'Region', placeholder: 'e.g. Luzon' },
                    { id: 'event', label: 'Event', placeholder: 'e.g. Contingency Case Congestion' },
                    { id: 'element', label: 'Element', placeholder: 'e.g. 3DASMA_TR1' },
                    { id: 'date', label: 'Date', placeholder: 'e.g. 09/25/2026' },
                    { id: 'interval', label: 'Interval', placeholder: 'e.g. 1140H and 1225H' },
                    { id: 'finding', label: 'Finding', type: 'textarea', placeholder: 'e.g. Reaching capacity to binding limit of 598MW...' },
                    { id: 'status', label: 'Status', type: 'textarea', placeholder: 'e.g. Upon simulation, congestion was not manifested.' }
                ]
            },
            base_case_congestion: {
                title: 'Base Case Congestion Notice',
                fields: [
                    { id: 'elementHeader', label: 'Header Element Identifier', placeholder: 'e.g. 14TACUR_TR4' },
                    { id: 'marketRun', label: 'Market Run', placeholder: 'e.g. RTD' },
                    { id: 'region', label: 'Region', placeholder: 'e.g. Mindanao' },
                    { id: 'event', label: 'Event', placeholder: 'e.g. Base Case Congestion' },
                    { id: 'element', label: 'Element', placeholder: 'e.g. 14TACUR_TR4' },
                    { id: 'date', label: 'Date', placeholder: 'e.g. 09/26/2026' },
                    { id: 'interval', label: 'Interval', placeholder: 'e.g. 0805H - 0900H' },
                    { id: 'finding', label: 'Finding', type: 'textarea', placeholder: 'e.g. Sudden increase of schedule of 14DSA_T2L1...' },
                    { id: 'status', label: 'Status', type: 'textarea', placeholder: 'e.g. At 0905H congestion was resolved.' }
                ]
            },
            load_curtailment: {
                title: 'Load Curtailment Notice',
                fields: [
                    { id: 'marketRun', label: 'Market Run', placeholder: 'e.g. RTD' },
                    { id: 'region', label: 'Region', placeholder: 'e.g. Visayas Grid' },
                    { id: 'event', label: 'Event', placeholder: 'e.g. Intermittent Load Curtailment' },
                    { id: 'magnitude', label: 'Magnitude', placeholder: 'e.g. 10.04-70.38 MW' },
                    { id: 'date', label: 'Date', placeholder: 'e.g. 09/26/2026' },
                    { id: 'intervals', label: 'Intervals Affected', placeholder: 'e.g. 1755H-1840H' },
                    { id: 'finding', label: 'Finding', type: 'textarea', placeholder: 'e.g. Generation deficiency.' },
                    { id: 'impact', label: 'Impact', placeholder: 'e.g. Possible PEN/Market Rerun' },
                    { id: 'status', label: 'Status', type: 'textarea', placeholder: 'e.g. MO on duty already notified CGO as of 1829H.' }
                ]
            }
        };

        let currentNoticeText = '';
        let manualBullets = [{ text: '', indent: false }];
        let isProcessing = false;

        function initTheme() {
            const savedTheme = localStorage.getItem('rto_theme') || 'light';
            document.documentElement.setAttribute('data-theme', savedTheme);
            updateThemeUI(savedTheme);
        }

        function toggleTheme() {
            const currentTheme = document.documentElement.getAttribute('data-theme') || 'light';
            const newTheme = currentTheme === 'light' ? 'dark' : 'light';
            document.documentElement.setAttribute('data-theme', newTheme);
            localStorage.setItem('rto_theme', newTheme);
            updateThemeUI(newTheme);
        }

        function updateThemeUI(theme) {
            document.getElementById('themeIcon').innerText = theme === 'dark' ? '☀️' : '🌙';
        }

        function renderFormFields() {
            const type = document.getElementById('noticeType').value;
            const container = document.getElementById('formFields');
            container.innerHTML = '';

            if (type === 'manual_notice') {
                renderManualEditor(container);
            } else {
                const schema = schemas[type];
                schema.fields.forEach(field => {
                    const group = document.createElement('div');
                    group.className = 'form-group';

                    const label = document.createElement('label');
                    label.innerText = field.label;
                    group.appendChild(label);

                    if (field.type === 'textarea') {
                        const textarea = document.createElement('textarea');
                        textarea.id = field.id;
                        textarea.placeholder = field.placeholder || '';
                        textarea.rows = 2;
                        textarea.oninput = updatePreview;
                        group.appendChild(textarea);
                    } else {
                        const input = document.createElement('input');
                        input.type = 'text';
                        input.id = field.id;
                        input.placeholder = field.placeholder || '';
                        input.oninput = updatePreview;
                        group.appendChild(input);
                    }

                    container.appendChild(group);
                });
            }

            updatePreview();
        }

        function renderManualEditor(container) {
            const titleGroup = document.createElement('div');
            titleGroup.className = 'form-group';
            const titleLabel = document.createElement('label');
            titleLabel.innerText = 'Custom Notice Title';
            const titleInput = document.createElement('input');
            titleInput.type = 'text';
            titleInput.id = 'manualTitle';
            titleInput.placeholder = 'e.g. System Advisory / Grid Status Note';
            titleInput.oninput = updatePreview;
            titleGroup.appendChild(titleLabel);
            titleGroup.appendChild(titleInput);
            container.appendChild(titleGroup);

            const bulletsLabel = document.createElement('label');
            bulletsLabel.innerText = 'Bullet Items & Operational Points';
            container.appendChild(bulletsLabel);

            const bulletsContainer = document.createElement('div');
            bulletsContainer.id = 'bulletsContainer';
            container.appendChild(bulletsContainer);

            const toolsDiv = document.createElement('div');
            toolsDiv.className = 'manual-tools';
            toolsDiv.innerHTML = `
                <button class="btn-sm" onclick="addBullet(false)">+ Add Main Bullet</button>
                <button class="btn-sm" onclick="addBullet(true)">↳ Add Sub-Bullet</button>
            `;
            container.appendChild(toolsDiv);

            refreshBulletRows();
        }

        function refreshBulletRows() {
            const container = document.getElementById('bulletsContainer');
            if (!container) return;
            container.innerHTML = '';

            manualBullets.forEach((item, idx) => {
                const row = document.createElement('div');
                row.className = `bullet-row ${item.indent ? 'indent-1' : ''}`;
                
                const bulletIcon = document.createElement('span');
                bulletIcon.style.fontSize = '0.8rem';
                bulletIcon.innerText = item.indent ? '▫' : '▪';
                row.appendChild(bulletIcon);

                const input = document.createElement('input');
                input.type = 'text';
                input.placeholder = item.indent ? 'Sub-detail...' : 'Main bullet note...';
                input.value = item.text;
                input.oninput = (e) => {
                    manualBullets[idx].text = e.target.value;
                    updatePreview();
                };
                row.appendChild(input);

                if (manualBullets.length > 1) {
                    const delBtn = document.createElement('button');
                    delBtn.className = 'bullet-row-btn';
                    delBtn.innerText = '✕';
                    delBtn.onclick = () => {
                        manualBullets.splice(idx, 1);
                        refreshBulletRows();
                        updatePreview();
                    };
                    row.appendChild(delBtn);
                }

                container.appendChild(row);
            });
        }

        function addBullet(isSub) {
            manualBullets.push({ text: '', indent: isSub });
            refreshBulletRows();
        }

        function updatePreview() {
            const type = document.getElementById('noticeType').value;
            let output = '';

            const getVal = (id) => {
                const el = document.getElementById(id);
                return el ? el.value.trim() : '';
            };

            if (type === 'manual_notice') {
                const title = getVal('manualTitle') || 'Grid Operations Notice';
                output = `${title}\n\n`;
                manualBullets.forEach(b => {
                    if (b.text.trim()) {
                        output += b.indent ? `   ▫ ${b.text.trim()}\n` : `▪ ${b.text.trim()}\n`;
                    }
                });
            } else {
                const schema = schemas[type];
                if (type === 'contingency_removal') {
                    output = `${schema.title}\n\n`;
                    if (getVal('marketRun')) output += `▪ Market Run: ${getVal('marketRun')}\n`;
                    if (getVal('effective')) output += `▪ Effective: ${getVal('effective')}\n`;
                    if (getVal('contingencyEquipment')) output += `▪ Contingency Equipment: ${getVal('contingencyEquipment')}\n`;
                    if (getVal('outageRelated')) output += `▪ Outage Related: ${getVal('outageRelated')}\n`;
                    if (getVal('outageDate')) output += `▪ Outage Date: ${getVal('outageDate')}\n`;
                    if (getVal('actualOnline')) output += `▪ Actual Online: ${getVal('actualOnline')}\n`;

                } else if (type === 'hvdc_limit') {
                    output = `${schema.title}\n\n`;
                    if (getVal('event')) output += `▪ Event: ${getVal('event')}\n`;
                    if (getVal('parameter')) output += `▪ Parameter: ${getVal('parameter')}\n`;
                    if (getVal('previousLimit')) output += `▪ Previous Limit: ${getVal('previousLimit')}\n`;
                    if (getVal('newLimit')) output += `▪ New Limit: ${getVal('newLimit')}\n`;
                    if (getVal('date')) output += `▪ Date: ${getVal('date')}\n`;
                    if (getVal('effective')) output += `▪ Effective: ${getVal('effective')}\n`;

                } else if (type === 'market_intervention') {
                    output = `${schema.title}\n\n`;
                    if (getVal('region')) output += `▪ Region: ${getVal('region')}\n`;
                    if (getVal('event')) output += `▪ Event: ${getVal('event')}\n`;
                    if (getVal('date')) output += `▪ Date: ${getVal('date')}\n`;
                    if (getVal('start')) output += `▪ Start: ${getVal('start')}\n`;
                    if (getVal('cause')) output += `▪ Cause: ${getVal('cause')}\n`;
                    if (getVal('marketImpact')) output += `▪ Market Impact: ${getVal('marketImpact')}\n`;
                    if (getVal('actionTaken')) output += `▪ Action Taken: ${getVal('actionTaken')}\n`;
                    output += `\nThank you.`;

                } else if (type === 'lifting_market_intervention') {
                    output = `${schema.title}\n\n`;
                    if (getVal('region')) output += `▪ Region: ${getVal('region')}\n`;
                    if (getVal('event')) output += `▪ Event: ${getVal('event')}\n`;
                    if (getVal('date')) output += `▪ Date: ${getVal('date')}\n`;
                    if (getVal('start')) output += `▪ Start: ${getVal('start')}\n`;
                    if (getVal('duration')) output += `▪ Duration: ${getVal('duration')}\n`;
                    if (getVal('cause')) output += `▪ Cause: ${getVal('cause')}\n`;
                    if (getVal('marketImpact')) output += `▪ Market Impact: ${getVal('marketImpact')}\n`;
                    if (getVal('actionTaken')) output += `▪ Action Taken: ${getVal('actionTaken')}\n`;

                } else if (type === 'contingency_congestion' || type === 'base_case_congestion') {
                    const elemHeader = getVal('elementHeader');
                    output = elemHeader ? `${schema.title} - ${elemHeader}\n\n` : `${schema.title}\n\n`;
                    if (getVal('marketRun')) output += `▪ Market Run: ${getVal('marketRun')}\n`;
                    if (getVal('region')) output += `▪ Region: ${getVal('region')}\n`;
                    if (getVal('event')) output += `▪ Event: ${getVal('event')}\n`;
                    if (getVal('element')) output += `▪ Element: ${getVal('element')}\n`;
                    if (getVal('date')) output += `▪ Date: ${getVal('date')}\n`;
                    if (getVal('interval')) output += `▪ Interval: ${getVal('interval')}\n`;
                    if (getVal('finding')) output += `▪ Finding: ${getVal('finding')}\n`;
                    if (getVal('status')) output += `▪ Status: ${getVal('status')}\n`;

                } else if (type === 'load_curtailment') {
                    const reg = getVal('region');
                    output = reg ? `${reg} Load Curtailment Notice\n\n` : `${schema.title}\n\n`;
                    if (getVal('marketRun')) output += `▪ Market Run: ${getVal('marketRun')}\n`;
                    if (getVal('region')) output += `▪ Region: ${getVal('region')}\n`;
                    if (getVal('event')) output += `▪ Event: ${getVal('event')}\n`;
                    if (getVal('magnitude')) output += `▪ Magnitude: ${getVal('magnitude')}\n`;
                    if (getVal('date')) output += `▪ Date: ${getVal('date')}\n`;
                    if (getVal('intervals')) output += `▪ Intervals affected: ${getVal('intervals')}\n`;
                    if (getVal('finding')) output += `▪ Finding: ${getVal('finding')}\n`;
                    if (getVal('impact')) output += `▪ Impact: ${getVal('impact')}\n`;
                    if (getVal('status')) output += `▪ Status: ${getVal('status')}\n`;
                }
            }

            const name = document.getElementById('reporterName').value.trim();
            const role = document.getElementById('reporterRole').value.trim();
            if (name) {
                output += role ? `\n\n▪ Reported by: ${name} (${role})` : `\n\n▪ Reported by: ${name}`;
            }

            currentNoticeText = output.trim();
            document.getElementById('previewText').innerText = currentNoticeText || 'Fill in form fields above to view preview...';
        }

        function saveReporterInfo() {
            localStorage.setItem('rto_reporter_name', document.getElementById('reporterName').value);
            localStorage.setItem('rto_reporter_role', document.getElementById('reporterRole').value);
        }

        function loadReporterInfo() {
            const name = localStorage.getItem('rto_reporter_name');
            const role = localStorage.getItem('rto_reporter_role');
            if (name) document.getElementById('reporterName').value = name;
            if (role) document.getElementById('reporterRole').value = role;
        }

        function getHistoryLog() {
            return JSON.parse(localStorage.getItem('rto_report_history') || '[]');
        }

        function saveReportToHistory() {
            const newLog = {
                id: Date.now(),
                timestamp: new Date().toLocaleString(),
                isoDate: new Date().toISOString(),
                type: document.getElementById('noticeType').value,
                reporter: document.getElementById('reporterName').value.trim(),
                role: document.getElementById('reporterRole').value.trim(),
                content: currentNoticeText
            };

            const logs = getHistoryLog();
            logs.unshift(newLog);
            localStorage.setItem('rto_report_history', JSON.stringify(logs));
            updateHistoryBadge();

            syncToGoogleSheet(newLog);
        }

        function syncToGoogleSheet(logData) {
            fetch(GOOGLE_SCRIPT_WEB_APP_URL, {
                method: 'POST',
                mode: 'no-cors',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify(logData)
            }).catch(err => {
                console.error('Google Sheets Sync Failure:', err);
            });
        }

        function updateHistoryBadge() {
            document.getElementById('historyBadge').innerText = getHistoryLog().length;
        }

        function openHistoryModal() {
            renderHistoryList();
            document.getElementById('historyModal').classList.add('active');
        }

        function closeHistoryModal() {
            document.getElementById('historyModal').classList.remove('active');
        }

        function showConfirmModal(title, subtitle) {
            document.getElementById('confirmTitle').innerText = title;
            document.getElementById('confirmSubtitle').innerText = subtitle;
            document.getElementById('confirmOverlay').classList.add('active');
        }

        function closeConfirmModal() {
            document.getElementById('confirmOverlay').classList.remove('active');
        }

        function renderHistoryList() {
            const container = document.getElementById('historyListContainer');
            const search = document.getElementById('historySearch').value.toLowerCase();
            const filterType = document.getElementById('historyFilterType').value;
            const sortOrder = document.getElementById('historySort').value;

            let logs = getHistoryLog();

            logs = logs.filter(item => {
                const matchesType = (filterType === 'ALL' || item.type === filterType);
                const matchesSearch = item.content.toLowerCase().includes(search) || item.reporter.toLowerCase().includes(search);
                return matchesType && matchesSearch;
            });

            logs.sort((a, b) => sortOrder === 'NEWEST' ? b.id - a.id : a.id - b.id);

            container.innerHTML = '';
            if (logs.length === 0) {
                container.innerHTML = `<p style="text-align: center; color: var(--text-muted); padding: 20px 0; font-size: 0.85rem;">No saved operational reports found.</p>`;
                return;
            }

            logs.forEach(log => {
                const card = document.createElement('div');
                card.className = 'history-card';
                card.innerHTML = `
                    <div class="history-card-header">
                        <span class="history-type">${log.type.replace('_', ' ')}</span>
                        <span class="history-date">${log.timestamp}</span>
                    </div>
                    <div class="history-body">${log.content}</div>
                    <div class="history-actions">
                        <button class="btn-sm" onclick="copyHistoryItem(${log.id})">📋 Copy</button>
                        <button class="btn-sm" style="color: #ef4444;" onclick="deleteHistoryItem(${log.id})">🗑️ Delete</button>
                    </div>
                `;
                container.appendChild(card);
            });
        }

        function copyHistoryItem(id) {
            const target = getHistoryLog().find(item => item.id === id);
            if (target) {
                copyTextToClipboard(target.content).then(() => {
                    showToast('Past report copied to clipboard!');
                });
            }
        }

        function deleteHistoryItem(id) {
            let logs = getHistoryLog();
            logs = logs.filter(item => item.id !== id);
            localStorage.setItem('rto_report_history', JSON.stringify(logs));
            updateHistoryBadge();
            renderHistoryList();
        }

        function clearAllHistory() {
            if (confirm('Are you sure you want to clear all report log history?')) {
                localStorage.removeItem('rto_report_history');
                updateHistoryBadge();
                renderHistoryList();
            }
        }

        function exportToGoogleSheetsCSV() {
            const logs = getHistoryLog();
            if (logs.length === 0) {
                alert('No report history available to export.');
                return;
            }

            let csvContent = "data:text/csv;charset=utf-8,ID,Timestamp,Notice Type,Reporter,Role,Content\n";
            logs.forEach(row => {
                const cleanContent = `"${row.content.replace(/"/g, '""')}"`;
                const cleanReporter = `"${row.reporter.replace(/"/g, '""')}"`;
                const cleanRole = `"${row.role.replace(/"/g, '""')}"`;
                csvContent += `${row.id},${row.timestamp},${row.type},${cleanReporter},${cleanRole},${cleanContent}\n`;
            });

            const encodedUri = encodeURI(csvContent);
            const link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", `RTO_Grid_Report_Log_${new Date().toISOString().slice(0,10)}.csv`);
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }

        function copyTextToClipboard(text) {
            return new Promise((resolve, reject) => {
                if (navigator.clipboard && window.isSecureContext) {
                    navigator.clipboard.writeText(text).then(resolve).catch(() => {
                        fallbackCopy(text) ? resolve() : reject();
                    });
                } else {
                    fallbackCopy(text) ? resolve() : reject();
                }
            });
        }

        function fallbackCopy(text) {
            const textArea = document.createElement("textarea");
            textArea.value = text;
            textArea.style.position = "fixed";
            textArea.style.left = "-999999px";
            document.body.appendChild(textArea);
            textArea.focus();
            textArea.select();
            let successful = false;
            try {
                successful = document.execCommand('copy');
            } catch (err) {
                successful = false;
            }
            document.body.removeChild(textArea);
            return successful;
        }

        function validateForm() {
            const reporterInput = document.getElementById('reporterName');
            if (!reporterInput.value.trim()) {
                reporterInput.classList.add('error-border');
                reporterInput.focus();
                showToast('Please enter Dispatcher Name before copying!');
                return false;
            }
            reporterInput.classList.remove('error-border');
            return true;
        }

        function disableButtons() {
            isProcessing = true;
            document.getElementById('btnCopyOnly').disabled = true;
            document.getElementById('btnCopyViber').disabled = true;
        }

        function enableButtons() {
            setTimeout(() => {
                isProcessing = false;
                document.getElementById('btnCopyOnly').disabled = false;
                document.getElementById('btnCopyViber').disabled = false;
            }, 1500); // 1.5 second rate-limit / debounce cooldown
        }

        function copyTextOnly() {
            if (isProcessing) return;
            if (!validateForm()) return;

            disableButtons();
            copyTextToClipboard(currentNoticeText).then(() => {
                saveReportToHistory();
                showConfirmModal(
                    "Report Text Copied!",
                    "The formatted operational notice is copied to your clipboard and synced to Google Sheets."
                );
            }).catch(() => {
                showToast('Failed to copy. Please copy manually.');
            }).finally(() => {
                enableButtons();
            });
        }

        function copyAndRedirectViber() {
            if (isProcessing) return;
            if (!validateForm()) return;

            disableButtons();
            copyTextToClipboard(currentNoticeText).then(() => {
                saveReportToHistory();
                showToast('Copied & Logged! Opening Viber...');
                setTimeout(() => {
                    window.location.href = "viber://";
                }, 500);
            }).catch(() => {
                showToast('Failed to copy text automatically.');
            }).finally(() => {
                enableButtons();
            });
        }

        function showToast(msg) {
            const toast = document.getElementById('toast');
            toast.innerText = msg;
            toast.classList.add('show');
            setTimeout(() => {
                toast.classList.remove('show');
            }, 2500);
        }

        window.onload = () => {
            initTheme();
            loadReporterInfo();
            renderFormFields();
            updateHistoryBadge();
        };
    </script>
</body>
</html>
