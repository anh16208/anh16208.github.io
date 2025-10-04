<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quản lý Thời gian</title>
    <style>
        :root {
            --primary-color: #4a6fa5;
            --secondary-color: #6b8cbc;
            --accent-color: #ff7e5f;
            --light-color: #f5f7fa;
            --dark-color: #333;
            --success-color: #28a745;
            --warning-color: #ffc107;
            --danger-color: #dc3545;
            --morning-color: #fff9c4;
            --afternoon-color: #e3f2fd;
            --evening-color: #f3e5f5;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--light-color);
            color: var(--dark-color);
            line-height: 1.6;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            background-color: var(--primary-color);
            color: white;
            padding: 1rem 0;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        .header-content {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        h1 {
            font-size: 1.8rem;
        }

        .date-display {
            font-size: 1.1rem;
        }

        .header-navigation {
            display: flex;
            gap: 10px;
        }

        .tab-switch-btn {
            background: rgba(255, 255, 255, 0.2);
            border: 1px solid rgba(255, 255, 255, 0.3);
            color: white;
            padding: 8px 15px;
            border-radius: 4px;
            cursor: pointer;
            transition: all 0.3s;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .tab-switch-btn:hover {
            background: rgba(255, 255, 255, 0.3);
        }

        .bell-icon {
            position: relative;
        }

        .notification-badge {
            position: absolute;
            top: -8px;
            right: -8px;
            background-color: var(--danger-color);
            color: white;
            border-radius: 50%;
            width: 18px;
            height: 18px;
            font-size: 0.7rem;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
        }

        .main-content {
            display: grid;
            grid-template-columns: 1fr;
            gap: 20px;
            margin-top: 20px;
        }

        @media (min-width: 768px) {
            .main-content {
                grid-template-columns: 1fr 1fr;
            }
        }

        @media (min-width: 1024px) {
            .main-content {
                grid-template-columns: 2fr 1fr;
            }
        }

        .card {
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            padding: 20px;
            margin-bottom: 20px;
        }

        .card h2 {
            margin-bottom: 15px;
            color: var(--primary-color);
            border-bottom: 2px solid var(--light-color);
            padding-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .form-group {
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
        }

        input, select, textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 1rem;
        }

        button {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1rem;
            transition: background-color 0.3s;
        }

        button:hover {
            background-color: var(--secondary-color);
        }

        .btn-success {
            background-color: var(--success-color);
        }

        .btn-warning {
            background-color: var(--warning-color);
            color: var(--dark-color);
        }

        .btn-danger {
            background-color: var(--danger-color);
        }

        .btn-primary {
            background-color: var(--primary-color);
            color: white;
        }

        .btn-primary:disabled {
            background-color: #28a745 !important;
            cursor: not-allowed;
            opacity: 0.7;
        }

        .add-subject-btn {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .task-list {
            list-style: none;
        }

        .task-item {
            background-color: var(--light-color);
            border-left: 4px solid var(--primary-color);
            padding: 15px;
            margin-bottom: 10px;
            border-radius: 4px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.3s ease;
        }

        .task-item:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }

        .task-item.completed {
            opacity: 0.7;
            border-left-color: var(--success-color);
        }

        .task-item.overdue {
            border-left-color: var(--danger-color);
        }

        .task-info h3 {
            margin-bottom: 5px;
        }

        .task-meta {
            font-size: 0.9rem;
            color: #666;
        }

        .task-actions {
            display: flex;
            gap: 5px;
        }

        .task-actions button {
            padding: 5px 10px;
            font-size: 0.9rem;
        }

        .priority-high {
            border-left-color: var(--danger-color);
        }

        .priority-medium {
            border-left-color: var(--warning-color);
        }

        .priority-low {
            border-left-color: var(--success-color);
        }

        .progress-bar {
            height: 10px;
            background-color: #e0e0e0;
            border-radius: 5px;
            margin-top: 10px;
            overflow: hidden;
        }

        .progress {
            height: 100%;
            background-color: var(--success-color);
            width: 0%;
            transition: width 0.5s;
        }

        .stats {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin-top: 15px;
        }

        .stat-card {
            background-color: var(--light-color);
            padding: 15px;
            border-radius: 8px;
            text-align: center;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .stat-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
        }

        .stat-value {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--primary-color);
        }

        .stat-label {
            font-size: 0.9rem;
            color: #666;
        }

        footer {
            text-align: center;
            margin-top: 30px;
            padding: 20px;
            color: #666;
            font-size: 0.9rem;
        }

        .empty-state {
            text-align: center;
            padding: 30px;
            color: #666;
        }

        .empty-state i {
            font-size: 3rem;
            margin-bottom: 15px;
            color: #ccc;
        }

        .timetable-container {
            overflow-x: auto;
            margin-top: 20px;
        }

        .timetable {
            width: 100%;
            border-collapse: collapse;
            min-width: 800px;
        }

        .timetable th, .timetable td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: center;
            font-size: 0.85rem;
        }

        .timetable th {
            background-color: var(--primary-color);
            color: white;
            font-weight: 600;
            position: sticky;
            top: 0;
            z-index: 10;
        }

        .timetable td {
            height: 60px;
            vertical-align: top;
            position: relative;
        }

        .time-slot {
            font-size: 0.75rem;
            color: #666;
            margin-bottom: 3px;
            white-space: nowrap;
        }

        .timetable-subject {
            background-color: var(--secondary-color);
            color: white;
            padding: 4px 6px;
            border-radius: 3px;
            margin-bottom: 3px;
            font-size: 0.8rem;
            cursor: pointer;
            transition: opacity 0.3s;
            word-break: break-word;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .timetable-subject:hover {
            opacity: 0.8;
        }

        .timetable-subject.high {
            background-color: var(--danger-color);
        }

        .timetable-subject.medium {
            background-color: var(--warning-color);
            color: var(--dark-color);
        }

        .timetable-subject.low {
            background-color: var(--success-color);
        }

        .tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 1px solid #ddd;
        }

        .tab {
            padding: 10px 20px;
            cursor: pointer;
            border-bottom: 3px solid transparent;
            transition: all 0.3s;
        }

        .tab.active {
            border-bottom: 3px solid var(--primary-color);
            color: var(--primary-color);
            font-weight: 600;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
        }

        .timetable-controls {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }

        .week-navigation {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .current-week {
            font-weight: 600;
            min-width: 150px;
            text-align: center;
        }

        .timetable-actions {
            display: flex;
            gap: 10px;
        }

        .time-period-column {
            background-color: #f8f9fa;
            font-weight: bold;
            text-align: center;
            width: 80px;
            writing-mode: vertical-lr;
            transform: rotate(180deg);
            vertical-align: middle;
        }

        .morning-period {
            background-color: var(--morning-color);
        }

        .afternoon-period {
            background-color: var(--afternoon-color);
        }

        .evening-period {
            background-color: var(--evening-color);
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }

        .modal-content {
            background-color: white;
            padding: 20px;
            border-radius: 8px;
            width: 90%;
            max-width: 800px;
            max-height: 90vh;
            overflow-y: auto;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }

        .close-modal {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: #666;
        }

        .timetable-form .form-group {
            margin-bottom: 15px;
        }

        .timetable-form .form-row {
            display: flex;
            gap: 15px;
        }

        .timetable-form .form-row .form-group {
            flex: 1;
        }

        .color-preview {
            width: 30px;
            height: 30px;
            border-radius: 4px;
            margin-top: 5px;
            border: 1px solid #ddd;
        }

        .time-selector {
            display: flex;
            gap: 10px;
            align-items: center;
            justify-content: center;
        }

        .time-column {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 5px;
        }

        .time-label {
            font-size: 0.8rem;
            color: #666;
            margin-bottom: 5px;
        }

        .time-dropdown {
            width: 80px;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 0.9rem;
            text-align: center;
        }

        .time-separator {
            font-size: 1.2rem;
            font-weight: bold;
            color: #333;
            margin-top: 15px;
            text-align: center;
        }

        .time-display {
            text-align: center;
            font-size: 1.1rem;
            font-weight: 600;
            margin: 10px 0;
            padding: 8px;
            background-color: #f8f9fa;
            border-radius: 4px;
        }

        .time-selector-group {
            margin-bottom: 15px;
        }

        .duration-display {
            font-size: 0.9rem;
            color: #666;
            margin-top: 5px;
            text-align: center;
        }

        .note-section {
            margin-top: 20px;
            padding-top: 15px;
            border-top: 1px solid #eee;
        }

        .note-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .note-toggle {
            background: none;
            border: none;
            color: var(--primary-color);
            cursor: pointer;
            font-size: 0.9rem;
            text-decoration: underline;
        }

        .note-content {
            display: none;
        }

        .note-content.show {
            display: block;
        }

        .note-textarea {
            min-height: 80px;
            resize: vertical;
        }

        .note-preview {
            background-color: #f8f9fa;
            padding: 10px;
            border-radius: 4px;
            border-left: 3px solid var(--primary-color);
            margin-top: 10px;
            font-size: 0.9rem;
            display: none;
        }

        .note-preview.show {
            display: block;
        }

        .timetable-indicator {
            margin-left: 8px;
            font-size: 0.9em;
            opacity: 0.8;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0% { opacity: 0.6; }
            50% { opacity: 1; }
            100% { opacity: 0.6; }
        }

        .notification-container {
            position: fixed;
            top: 20px;
            right: 20px;
            z-index: 1001;
            max-width: 400px;
        }

        .notification {
            background: white;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
            margin-bottom: 10px;
            padding: 15px;
            display: flex;
            align-items: flex-start;
            gap: 12px;
            transform: translateX(400px);
            transition: transform 0.3s ease;
            border-left: 4px solid var(--primary-color);
        }

        .notification.show {
            transform: translateX(0);
        }

        .notification-icon {
            font-size: 1.5rem;
            flex-shrink: 0;
        }

        .notification-content {
            flex: 1;
        }

        .notification-title {
            font-weight: 600;
            margin-bottom: 5px;
            color: var(--dark-color);
        }

        .notification-message {
            font-size: 0.9rem;
            color: #666;
            margin-bottom: 8px;
            white-space: pre-line;
        }

        .notification-time {
            font-size: 0.8rem;
            color: #999;
        }

        .notification-close {
            background: none;
            border: none;
            font-size: 1.2rem;
            cursor: pointer;
            color: #999;
            padding: 0;
            width: 24px;
            height: 24px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .notification-close:hover {
            color: var(--danger-color);
        }

        .notification.success {
            border-left-color: var(--success-color);
        }

        .notification.warning {
            border-left-color: var(--warning-color);
        }

        .notification.error {
            border-left-color: var(--danger-color);
        }

        .notification.info {
            border-left-color: var(--primary-color);
        }

        .study-notification {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border-left: 4px solid #ff7e5f;
        }

        .study-notification .notification-icon {
            font-size: 1.8rem;
        }

        .study-actions {
            display: flex;
            gap: 8px;
            margin-top: 10px;
            flex-wrap: wrap;
        }

        .study-action-btn {
            padding: 6px 12px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 0.8rem;
            transition: all 0.3s;
            flex: 1;
            min-width: 80px;
        }

        .study-action-btn.postpone {
            background: rgba(255, 255, 255, 0.2);
            color: white;
            border: 1px solid rgba(255, 255, 255, 0.3);
        }

        .study-action-btn.postpone:hover {
            background: rgba(255, 255, 255, 0.3);
        }

        .study-action-btn.start {
            background: #28a745;
            color: white;
        }

        .study-action-btn.start:hover {
            background: #218838;
        }

        .study-action-btn.skip {
            background: #dc3545;
            color: white;
        }

        .study-action-btn.skip:hover {
            background: #c82333;
        }

        .countdown-timer {
            font-size: 1.2rem;
            font-weight: bold;
            text-align: center;
            margin: 10px 0;
            padding: 8px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 4px;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .upcoming-classes {
            margin-top: 15px;
            padding-top: 10px;
            border-top: 1px solid rgba(255, 255, 255, 0.2);
        }

        .upcoming-class {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 5px 0;
            font-size: 0.85rem;
        }

        .class-time {
            font-weight: bold;
        }

        .class-subject {
            flex: 1;
            margin: 0 10px;
        }

        .settings-panel {
            position: fixed;
            top: 0;
            right: -400px;
            width: 400px;
            height: 100vh;
            background: white;
            box-shadow: -2px 0 10px rgba(0,0,0,0.1);
            transition: right 0.3s ease;
            z-index: 1002;
            padding: 20px;
            overflow-y: auto;
        }

        .settings-panel.open {
            right: 0;
        }

        .settings-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #eee;
        }

        .settings-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1001;
            display: none;
        }

        .settings-overlay.show {
            display: block;
        }

        .stats-details {
            margin-top: 20px;
        }

        .stats-tabs {
            display: flex;
            margin-bottom: 15px;
            border-bottom: 1px solid #ddd;
        }

        .stats-tab {
            padding: 10px 20px;
            cursor: pointer;
            border-bottom: 3px solid transparent;
            transition: all 0.3s;
        }

        .stats-tab.active {
            border-bottom: 3px solid var(--primary-color);
            color: var(--primary-color);
            font-weight: 600;
        }

        .stats-content {
            display: none;
        }

        .stats-content.active {
            display: block;
        }

        .subject-stats {
            margin-bottom: 20px;
        }

        .subject-stat-item {
            background: var(--light-color);
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 10px;
            border-left: 4px solid var(--primary-color);
        }

        .subject-stat-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .subject-name {
            font-weight: 600;
            font-size: 1.1rem;
        }

        .subject-total-time {
            font-weight: 600;
            color: var(--primary-color);
        }

        .day-stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .day-stat-item {
            background: var(--light-color);
            padding: 15px;
            border-radius: 8px;
            text-align: center;
            border-left: 4px solid var(--success-color);
        }

        .day-name {
            font-weight: 600;
            margin-bottom: 5px;
        }

        .day-study-time {
            font-size: 1.2rem;
            font-weight: bold;
            color: var(--primary-color);
        }

        .day-subject-count {
            font-size: 0.9rem;
            color: #666;
            margin-top: 5px;
        }

        .progress-details {
            margin-top: 10px;
        }

        .progress-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 8px;
            padding: 8px;
            background: white;
            border-radius: 4px;
        }

        .progress-subject {
            font-weight: 500;
        }

        .progress-bar-small {
            flex: 1;
            height: 8px;
            background-color: #e0e0e0;
            border-radius: 4px;
            margin: 0 10px;
            overflow: hidden;
        }

        .progress-small {
            height: 100%;
            background-color: var(--success-color);
            width: 0%;
            transition: width 0.5s;
        }

        .progress-percent {
            font-weight: 600;
            color: var(--primary-color);
            min-width: 40px;
            text-align: right;
        }

        .timetable-detailed td {
            height: 30px;
        }

        .time-slot-small {
            font-size: 0.7rem;
            color: #666;
        }

        .timetable-subject-small {
            font-size: 0.7rem;
            padding: 2px 4px;
        }

        @media (max-width: 768px) {
            .timetable {
                min-width: 1000px;
            }
            
            .time-selector {
                flex-direction: column;
                gap: 15px;
            }
            
            .time-separator {
                margin: 5px 0;
            }
            
            .header-content {
                flex-direction: column;
                gap: 15px;
            }
            
            .header-navigation {
                flex-direction: column;
                gap: 5px;
            }
            
            .tab-switch-btn {
                padding: 5px 10px;
                font-size: 0.9rem;
            }
            
            .task-actions {
                flex-direction: column;
            }

            .notification-container {
                right: 10px;
                left: 10px;
                max-width: none;
            }

            .settings-panel {
                width: 100%;
                right: -100%;
            }

            .time-period-column {
                width: 60px;
                font-size: 0.7rem;
            }

            .stats {
                grid-template-columns: 1fr;
            }

            .day-stats-grid {
                grid-template-columns: 1fr;
            }

            .study-actions {
                flex-direction: column;
            }

            .study-action-btn {
                min-width: auto;
            }
        }

        body[data-theme="dark"] {
            --light-color: #2d3748;
            --dark-color: #f7fafc;
            background-color: #1a202c;
            color: #f7fafc;
        }

        body[data-theme="dark"] .card {
            background: #2d3748;
            color: #f7fafc;
        }

        body[data-theme="dark"] input,
        body[data-theme="dark"] select,
        body[data-theme="dark"] textarea {
            background: #4a5568;
            color: #f7fafc;
            border-color: #718096;
        }

        .notification-permission-prompt {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: white;
            border: 2px solid var(--primary-color);
            border-radius: 8px;
            padding: 15px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
            z-index: 1003;
            max-width: 300px;
        }

        .notification-permission-prompt h4 {
            margin-bottom: 10px;
            color: var(--primary-color);
        }

        .notification-permission-buttons {
            display: flex;
            gap: 10px;
            margin-top: 10px;
        }

        .notification-permission-buttons button {
            flex: 1;
            padding: 8px 12px;
            font-size: 0.9rem;
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <div class="header-content">
                <h1>📚 Quản lý Thời gian</h1>
                <div class="header-navigation">
                    <button onclick="switchToTab('tasks')" class="tab-switch-btn">📚 Môn học</button>
                    <button onclick="switchToTab('timetable')" class="tab-switch-btn">📅 Thời khóa biểu</button>
                    <button onclick="showTodaysSchedule()" class="tab-switch-btn">📋 Lịch hôm nay</button>
                    <button onclick="openSettings()" class="tab-switch-btn bell-icon" id="settingsBtn">
                        ⚙️ Cài đặt
                        <span class="notification-badge" id="settingsBadge" style="display: none;"></span>
                    </button>
                </div>
                <div class="date-display" id="currentDate"></div>
            </div>
        </div>
    </header>

    <div class="container">
        <div class="tabs">
            <div class="tab active" data-tab="tasks">Quản lý Môn học</div>
            <div class="tab" data-tab="timetable">Thời khóa biểu</div>
        </div>

        <div class="tab-content active" id="tasks-tab">
            <div class="main-content">
                <div class="left-column">
                    <div class="card">
                        <h2>🔔 Thêm môn học mới</h2>
                        <form id="taskForm">
                            <div class="form-group">
                                <label for="taskName">Tên môn HK</label>
                                <input type="text" id="taskName" required>
                            </div>
                            <div class="form-group">
                                <label for="taskDescription">Mô tả</label>
                                <textarea id="taskDescription" rows="3"></textarea>
                            </div>
                            <div class="form-group">
                                <label for="taskDueDate">Thời hạn</label>
                                <input type="datetime-local" id="taskDueDate" required>
                            </div>
                            <div class="form-group">
                                <label for="taskPriority">Mức độ ưu tiên</label>
                                <select id="taskPriority">
                                    <option value="low">Thấp</option>
                                    <option value="medium" selected>Trung bình</option>
                                    <option value="high">Cao</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label for="taskDuration">Thời lượng học (phút)</label>
                                <input type="number" id="taskDuration" min="1" value="60">
                            </div>
                            <button type="submit" class="btn-success add-subject-btn">
                                🔔 Thêm môn học
                            </button>
                        </form>
                    </div>

                    <div class="card">
                        <h2>📚 Lịch học </h2>
                        <div id="taskList">
                            <div class="empty-state">
                                <i>📚</i>
                                <p>Chưa có môn học nào. </p>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="right-column">
                    <div class="card">
                        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px;">
                            <h2 style="margin-bottom: 0;">📊 Thống kê </h2>
                            <button onclick="showStatsDetails()" class="btn-primary" style="padding: 8px 12px; font-size: 0.9rem;">
                                📊 Xem chi tiết
                            </button>
                        </div>
                        <div class="stats">
                            <div class="stat-card" onclick="showStatsDetails('subjects')">
                                <div class="stat-value" id="totalTasks">0</div>
                                <div class="stat-label">Tổng môn học</div>
                            </div>
                            <div class="stat-card" onclick="showStatsDetails('completion')">
                                <div class="stat-value" id="completedTasks">0</div>
                                <div class="stat-label">Đã hoàn thành</div>
                            </div>
                            <div class="stat-card" onclick="showStatsDetails('pending')">
                                <div class="stat-value" id="pendingTasks">0</div>
                                <div class="stat-label">Chưa hoàn thành</div>
                            </div>
                            <div class="stat-card" onclick="showStatsDetails('time')">
                                <div class="stat-value" id="studyTime">0h</div>
                                <div class="stat-label">Tổng thời gian học</div>
                            </div>
                        </div>
                        <div class="progress-container" style="margin-top: 20px;">
                            <div class="progress-bar">
                                <div class="progress" id="progressBar"></div>
                            </div>
                            <div style="text-align: center; margin-top: 5px;">
                                <span id="progressText">0% hoàn thành</span>
                            </div>
                        </div>
                    </div>

                    <div class="card">
                        <h2>⏰ Môn học sắp đến hạn</h2>
                        <div id="upcomingTasks">
                            <div class="empty-state">
                                <i>⏰</i>
                                <p>Không có môn học nào sắp đến hạn</p>
                            </div>
                        </div>
                    </div>

                    <div class="card">
                        <h2>💡 Lời khuyên học tập</h2>
                        <ul id="studyTips">
                        <!--Thêm lời khuyên <li>......</li>--> 
                            <li></li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>

        <div class="tab-content" id="timetable-tab">
            <div class="card">
                <div class="timetable-controls">
                    <div class="week-navigation">
                        <button id="prevWeek">‹</button>
                        <div class="current-week" id="currentWeek"></div>
                        <button id="nextWeek">›</button>
                    </div>
                    <div class="timetable-actions">
                        <button id="addToTimetable" class="btn-success">Thêm vào TKB</button>
                        <button id="clearTimetable" class="btn-danger">Xóa TKB</button>
                        <button id="toggleView" class="btn-primary" onclick="toggleTimetableView()">📊 Xem chi tiết</button>
                    </div>
                </div>
                <div class="timetable-container">
                    <table class="timetable" id="timetable">
                        <thead>
                            <tr>
                                <th style="width: 80px;">Buổi</th>
                                <th style="width: 80px;">Giờ</th>
                                <th>Thứ 2</th>
                                <th>Thứ 3</th>
                                <th>Thứ 4</th>
                                <th>Thứ 5</th>
                                <th>Thứ 6</th>
                                <th>Thứ 7</th>
                                <th>Chủ nhật</th>
                            </tr>
                        </thead>
                        <tbody id="timetableBody">
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal Thống kê  -->
    <div class="modal" id="statsModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>📊 Thống kê học tập </h2>
                <button class="close-modal" onclick="closeStatsModal()">&times;</button>
            </div>
            
            <div class="stats-tabs">
                <div class="stats-tab active" data-tab="subjects">Theo môn học</div>
                <div class="stats-tab" data-tab="days">Theo ngày trong tuần</div>
                <div class="stats-tab" data-tab="completion">Tiến độ hoàn thành</div>
                <div class="stats-tab" data-tab="performance">Hiệu suất học tập</div>
            </div>
            
            <div class="stats-content active" id="subjects-stats">
                <h3>Thống kê theo môn học</h3>
                <div id="subjectStatsList">
                </div>
            </div>
            
            <div class="stats-content" id="days-stats">
                <h3>Thống kê theo ngày trong tuần</h3>
                <div class="day-stats-grid" id="dayStatsGrid">
                </div>
            </div>
            
            <div class="stats-content" id="completion-stats">
                <h3>Tiến độ hoàn thành môn học</h3>
                <div class="progress-details" id="completionProgress">
                </div>
            </div>

            <div class="stats-content" id="performance-stats">
                <h3>Hiệu suất học tập</h3>
                <div class="stats" style="margin-bottom: 20px;">
                    <div class="stat-card">
                        <div class="stat-value" id="avgStudyTime">0h</div>
                        <div class="stat-label">Thời gian học trung bình/ngày</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-value" id="efficiencyScore">0%</div>
                        <div class="stat-label">Hiệu suất học tập</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-value" id="consistencyScore">0%</div>
                        <div class="stat-label">Độ ổn định</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-value" id="focusTime">0h</div>
                        <div class="stat-label">Thời gian tập trung cao</div>
                    </div>
                </div>
                <div class="card">
                    <h4>📈 Phân tích học tập</h4>
                    <div id="performanceAnalysis">
                    </div>
                </div>
            </div>
        </div>
    </div>

    <div class="notification-container" id="notificationContainer"></div>

    <div class="settings-overlay" id="settingsOverlay"></div>
    <div class="settings-panel" id="settingsPanel">
        <div class="settings-header">
            <h2>Cài đặt Hệ thống</h2>
            <button class="close-modal" onclick="closeSettings()">&times;</button>
        </div>
        
        <div class="form-group">
            <h3>🔔 Cài đặt Thông báo</h3>
            <label>
                <input type="checkbox" id="enableNotifications" checked>
                Bật thông báo
            </label>
        </div>
        
        <div class="form-group">
            <label>
                <input type="checkbox" id="enableDesktopNotifications" checked>
                Bật thông báo trên desktop/mobile
            </label>
            <small style="display: block; color: #666; margin-top: 5px;">
                Hiển thị thông báo ngay cả khi trình duyệt không active
            </small>
        </div>
        
        <div class="form-group">
            <label for="notificationTime">Thời gian thông báo trước (phút)</label>
            <select id="notificationTime">
                <option value="5">5 phút</option>
                <option value="10">10 phút</option>
                <option value="15" selected>15 phút</option>
                <option value="30">30 phút</option>
                <option value="60">1 giờ</option>
            </select>
        </div>
        
        <div class="form-group">
            <label for="notificationSound">Âm thanh thông báo</label>
            <select id="notificationSound">
                <option value="none">Không có âm thanh</option>
                <option value="default" selected>Âm thanh mặc định</option>
                <option value="bell">Chuông</option>
                <option value="chime">Tiếng chuông nhẹ</option>
            </select>
        </div>

        <div class="form-group">
            <h3>🎨 Cài đặt Giao diện</h3>
            <label for="themeSelect">Chủ đề giao diện</label>
            <select id="themeSelect">
                <option value="light">Sáng</option>
                <option value="dark">Tối</option>
                <option value="auto">Tự động</option>
            </select>
        </div>

        <div class="form-group">
            <label for="languageSelect">Ngôn ngữ</label>
            <select id="languageSelect">
                <option value="vi">Tiếng Việt</option>
                <option value="en">English</option>
            </select>
        </div>

        <div class="form-group">
            <label>
                <input type="checkbox" id="autoSync" checked>
                Đồng bộ hóa tự động
            </label>
        </div>

        <div class="form-group">
            <h3>📊 Cài đặt Thống kê</h3>
            <label>
                <input type="checkbox" id="trackStudyTime" checked>
                Theo dõi thời gian học
            </label>
        </div>

        <div class="form-group">
            <label>
                <input type="checkbox" id="showProductivityTips" checked>
                Hiển thị mẹo học tập
            </label>
        </div>

        <div class="form-group">
            <label for="studyGoal">Mục tiêu học tập hàng ngày (phút)</label>
            <input type="number" id="studyGoal" min="30" value="120">
        </div>

        <div class="form-group">
            <h3>🛠️ Cài đặt Nâng cao</h3>
            <label>
                <input type="checkbox" id="enableDebugMode">
                Chế độ gỡ lỗi
            </label>
        </div>

        <div class="form-group">
            <label for="dataRetention">Thời gian lưu dữ liệu</label>
            <select id="dataRetention">
                <option value="7">1 tuần</option>
                <option value="30" selected>1 tháng</option>
                <option value="90">3 tháng</option>
                <option value="365">1 năm</option>
                <option value="forever">Mãi mãi</option>
            </select>
        </div>
        
        <div class="form-group">
            <button class="btn-success" onclick="testNotification()">Kiểm tra thông báo</button>
            <button class="btn-warning" onclick="exportData()">Xuất dữ liệu</button>
            <button class="btn-danger" onclick="clearAllData()">Xóa tất cả dữ liệu</button>
        </div>
        
        <div class="form-group">
            <h3>📋 Lịch sử thông báo</h3>
            <div id="notificationHistory" style="max-height: 200px; overflow-y: auto; background: #f8f9fa; padding: 10px; border-radius: 4px;">
            </div>
        </div>

        <div class="form-group">
            <h3>ℹ️ Thông tin Ứng dụng</h3>
            <div style="background: #f8f9fa; padding: 15px; border-radius: 4px;">
                <p><strong>Phiên bản:</strong> 2.0.0</p>
                <p><strong>Dung lượng dữ liệu:</strong> <span id="storageUsage">0 KB</span></p>
                <p><strong>Số môn học:</strong> <span id="totalSubjectsCount">0</span></p>
                <p><strong>Số giờ học:</strong> <span id="totalStudyHours">0</span></p>
            </div>
        </div>
    </div>

    <div class="modal" id="timetableModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2 id="timetableModalTitle">Thêm môn học vào thời khóa biểu</h2>
                <button class="close-modal">&times;</button>
            </div>
            <form id="timetableForm" class="timetable-form">
                <input type="hidden" id="editMode" value="false">
                <input type="hidden" id="editTimetableId" value="">
                <input type="hidden" id="editDay" value="">
                <input type="hidden" id="editWeekKey" value="">
                
                <div class="form-group">
                    <label for="timetableSubject">Môn học</label>
                    <select id="timetableSubject" required>
                        <option value="">Chọn môn học</option>
                    </select>
                </div>
                
                <div class="form-group">
                    <label for="subjectDescription">Mô tả môn học</label>
                    <textarea id="subjectDescription" rows="2" placeholder="Mô tả về môn học..."></textarea>
                </div>
                
                <div class="form-row">
                    <div class="form-group">
                        <label for="timetableDay">Thứ</label>
                        <select id="timetableDay" required>
                            <option value="1">Thứ 2</option>
                            <option value="2">Thứ 3</option>
                            <option value="3">Thứ 4</option>
                            <option value="4">Thứ 5</option>
                            <option value="5">Thứ 6</option>
                            <option value="6">Thứ 7</option>
                            <option value="0">Chủ nhật</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="subjectPriority">Mức độ ưu tiên</label>
                        <select id="subjectPriority">
                            <option value="low">Thấp</option>
                            <option value="medium" selected>Trung bình</option>
                            <option value="high">Cao</option>
                        </select>
                    </div>
                </div>
                
                <div class="form-group">
                    <label>Thời gian học (24h)</label>
                    
                    <!-- Bắt đầu -->
                    <div class="time-selector-group">
                        <label class="time-label">Bắt đầu</label>
                        <div class="time-selector">
                            <div class="time-column">
                                <select class="time-dropdown" id="startHour">
                                </select>
                                <div class="time-label">Giờ</div>
                            </div>
                            <div class="time-column">
                                <select class="time-dropdown" id="startMinute">
                                </select>
                                <div class="time-label">Phút</div>
                            </div>
                        </div>
                    </div>

                    <div class="time-separator">→</div>

                    <!-- Kết thúc -->
                    <div class="time-selector-group">
                        <label class="time-label">Kết thúc</label>
                        <div class="time-selector">
                            <div class="time-column">
                                <select class="time-dropdown" id="endHour">
                                </select>
                                <div class="time-label">Giờ</div>
                            </div>
                            <div class="time-column">
                                <select class="time-dropdown" id="endMinute">
                                </select>
                                <div class="time-label">Phút</div>
                            </div>
                        </div>
                    </div>

                    <div class="time-display" id="timeDisplay">
                        Thời gian: 07:00 - 08:00
                    </div>
                    <div class="duration-display" id="durationDisplay">Thời lượng: 1 giờ 0 phút</div>
                </div>

                <!-- Phần ghi -->
                <div class="note-section">
                    <div class="note-header">
                        <label style="margin-bottom: 0;">Ghi chú cho buổi học</label>
                        <button type="button" class="note-toggle" id="noteToggle">
                            + Thêm ghi chú
                        </button>
                    </div>
                    <div class="note-content" id="noteContent">
                        <textarea 
                            id="timetableNote" 
                            class="note-textarea" 
                            placeholder="Thêm ghi chú cho buổi học này... (ví dụ: bài cần học, trang cần đọc, bài tập cần làm...)"
                            rows="4"
                        ></textarea>
                        <div class="note-preview" id="notePreview">
                            <strong>Ghi chú:</strong> <span id="notePreviewText"></span>
                        </div>
                    </div>
                </div>

                <div class="form-group">
                    <label for="timetableColor">Màu sắc</label>
                    <select id="timetableColor">
                        <option value="#ff7e5f">Cam</option>
                        <option value="#e83e8c">Hồng</option>
                        <option value="#20c997">Xanh ngọc</option>
                    </select>
                    <div class="color-preview" id="colorPreview" style="background-color: #4a6fa5;"></div>
                </div>
                
                <div class="form-group">
                    <label>
                        <input type="checkbox" id="autoCreateTask" checked>
                        Tự động thêm vào Lịch học của tôi
                    </label>
                    <small style="display: block; color: #666; margin-top: 5px;">
                        Khi được chọn, môn học sẽ tự động được thêm vào danh sách Lịch học của tôi với thời hạn là ngày học.
                    </small>
                </div>
                
                <div class="form-group" id="editActions" style="display: none;">
                    <div class="form-row">
                        <button type="button" class="btn-danger" id="deleteSubjectBtn" style="flex: 1;">Xóa môn học</button>
                        <button type="button" class="btn-warning" id="cancelEditBtn" style="flex: 1;">Hủy chỉnh sửa</button>
                    </div>
                </div>
                
                <div class="form-row">
                    <button type="submit" class="btn-success" id="submitTimetableBtn" style="flex: 1;">Thêm vào TKB</button>
                    <button type="button" class="btn-primary" onclick="closeTimetableModal()" style="flex: 1;">Đóng</button>
                </div>
            </form>
        </div>
    </div>

    <footer>
        <div class="container">
            <p>Anh1620</p>
        </div>
    </footer>

    <script>
        //  3 MÔN HỌC
        const defaultSubjects = [
            { id: 'math', name: 'Toán', description: 'Môn Toán học' },
            { id: 'physics', name: 'Lý', description: 'Môn Vật lý' },
            { id: 'english', name: 'Anh', description: 'Môn Tiếng Anh' }
        ];

        // Biến để lưu thời gian
        let startTime24h = "07:00";
        let endTime24h = "08:00";
        let isDetailedView = false;
        let currentWeek = 0;

        // THÔNG BÁO HỌC TẬP
        let studyNotificationInterval;
        let currentStudySession = null;
        let studySessionStartTime = null;
        let postponedSessions = [];

        // App settings
        let appSettings = {
            notifications: {
                enabled: true,
                desktopEnabled: true,
                timeBefore: 15,
                sound: 'default'
            },
            appearance: {
                theme: 'light',
                language: 'vi'
            },
            study: {
                trackStudyTime: true,
                showProductivityTips: true,
                dailyGoal: 120,
                autoSync: true
            },
            advanced: {
                debugMode: false,
                dataRetention: 30
            }
        };

        // Thông báo
        function requestNotificationPermission() {
            if (!("Notification" in window)) {
                console.log("Trình duyệt này không hỗ trợ thông báo desktop");
                return false;
            }
            
            if (Notification.permission === "granted") {
                return true;
            } else if (Notification.permission !== "denied") {
                Notification.requestPermission().then(permission => {
                    if (permission === "granted") {
                        console.log("Đã cấp quyền thông báo desktop");
                        showNotification("Thành công", "Đã bật thông báo desktop", "success");
                        return true;
                    }
                });
            }
            return false;
        }

        function showDesktopNotification(title, message, icon = null) {
            if (!appSettings.notifications.desktopEnabled) return;
            
            if (!requestNotificationPermission()) return;
            
            const options = {
                body: message,
                icon: icon || '/favicon.ico',
                badge: '/favicon.ico',
                tag: 'study-manager',
                requireInteraction: false,
                silent: appSettings.notifications.sound === 'none'
            };
            
            if ('actions' in Notification.prototype) {
                options.actions = [
                    {
                        action: 'open',
                        title: 'Mở ứng dụng'
                    },
                    {
                        action: 'snooze',
                        title: 'Hoãn 5 phút'
                    }
                ];
            }
            
            const notification = new Notification(title, options);
            
            notification.onclick = function() {
                window.focus();
                notification.close();
                switchToTab('tasks');
            };
            
            notification.onclose = function() {
                console.log('Thông báo đã đóng');
            };
            
            // Xử lý actions (nếu có)
            if (notification.actions) {
                notification.addEventListener('notificationclick', function(event) {
                    event.notification.close();
                    
                    if (event.action === 'open') {
                        window.focus();
                        switchToTab('tasks');
                    } else if (event.action === 'snooze') {
                        // Xử lý hoãn thông báo
                        showNotification("Đã hoãn", "Thông báo đã được hoãn 5 phút", "warning");
                    }
                });
            }
            
            // Tự động đóng thông báo
            setTimeout(() => {
                notification.close();
            }, 10000); //tg
            
            return notification;
        }

        // Hiển thị ngày hiện tại
        function updateCurrentDate() {
            const now = new Date();
            const options = { 
                weekday: 'long', 
                year: 'numeric', 
                month: 'long', 
                day: 'numeric' 
            };
            document.getElementById('currentDate').textContent = now.toLocaleDateString('vi-VN', options);
        }

        // Lưu và tải dữ liệu từ localStorage
        function saveTasksToStorage(tasks) {
            localStorage.setItem('studyTasks', JSON.stringify(tasks));
        }

        function loadTasksFromStorage() {
            const tasks = localStorage.getItem('studyTasks');
            return tasks ? JSON.parse(tasks) : [];
        }

        function saveTimetableToStorage(timetable) {
            localStorage.setItem('studyTimetable', JSON.stringify(timetable));
        }

        function loadTimetableFromStorage() {
            const timetable = localStorage.getItem('studyTimetable');
            return timetable ? JSON.parse(timetable) : {};
        }

        function saveAppSettings(settings) {
            localStorage.setItem('appSettings', JSON.stringify(settings));
        }

        function loadAppSettings() {
            const settings = localStorage.getItem('appSettings');
            return settings ? JSON.parse(settings) : appSettings;
        }

        // Tạo ID duy nhất cho mỗi task
        function generateId() {
            return Date.now().toString(36) + Math.random().toString(36).substr(2);
        }

        // Định dạng ngày giờ
        function formatDateTime(dateTimeString) {
            const date = new Date(dateTimeString);
            return date.toLocaleString('vi-VN');
        }

        // Tính toán thời gian còn lại
        function getTimeRemaining(dueDate) {
            const now = new Date();
            const due = new Date(dueDate);
            const diff = due - now;
            
            if (diff <= 0) return 'Đã quá hạn';
            
            const days = Math.floor(diff / (1000 * 60 * 60 * 24));
            const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
            
            if (days > 0) return `${days} ngày ${hours} giờ`;
            if (hours > 0) return `${hours} giờ ${minutes} phút`;
            return `${minutes} phút`;
        }

        // Thông báo
        function showNotification(title, message, type = 'info', duration = 5000) {
            if (!appSettings.notifications.enabled) return;

            // Phát âm thanh thông báo
            playNotificationSound(type);

            // Hiển thị thông báo
            if (Notification.permission === "granted" && appSettings.notifications.desktopEnabled) {
                showDesktopNotification(title, message);
            }

            const notificationContainer = document.getElementById('notificationContainer');
            const notificationId = generateId();
            
            const notification = document.createElement('div');
            notification.className = `notification ${type}`;
            notification.id = `notification-${notificationId}`;
            
            const icons = {
                info: '🔔',
                warning: '⚠️',
                error: '❌',
                success: '✅'
            };
            
            notification.innerHTML = `
                <div class="notification-icon">${icons[type]}</div>
                <div class="notification-content">
                    <div class="notification-title">${title}</div>
                    <div class="notification-message">${message}</div>
                    <div class="notification-time">${new Date().toLocaleTimeString('vi-VN')}</div>
                </div>
                <button class="notification-close" onclick="closeNotification('${notificationId}')">&times;</button>
            `;
            
            notificationContainer.appendChild(notification);
            
            setTimeout(() => {
                notification.classList.add('show');
            }, 100);
            
            if (duration > 0) {
                setTimeout(() => {
                    closeNotification(notificationId);
                }, duration);
            }
            
            return notificationId;
        }

        function closeNotification(notificationId) {
            const notification = document.getElementById(`notification-${notificationId}`);
            if (notification) {
                notification.classList.remove('show');
                setTimeout(() => {
                    if (notification.parentNode) {
                        notification.parentNode.removeChild(notification);
                    }
                }, 300);
            }
        }

        // Phát âm thanh thông báo
        function playNotificationSound(type = 'default') {
            if (!appSettings.notifications.enabled || appSettings.notifications.sound === 'none') return;
            
            // Tạo âm thanh thông báo bằng Web Audio API
            try {
                const audioContext = new (window.AudioContext || window.webkitAudioContext)();
                const oscillator = audioContext.createOscillator();
                const gainNode = audioContext.createGain();
                
                oscillator.connect(gainNode);
                gainNode.connect(audioContext.destination);
                
                switch(appSettings.notifications.sound) {
                    case 'bell':
                        oscillator.type = 'sine';
                        oscillator.frequency.setValueAtTime(800, audioContext.currentTime);
                        oscillator.frequency.setValueAtTime(600, audioContext.currentTime + 0.1);
                        break;
                    case 'chime':
                        oscillator.type = 'triangle';
                        oscillator.frequency.setValueAtTime(523.25, audioContext.currentTime); 
                        oscillator.frequency.setValueAtTime(659.25, audioContext.currentTime + 0.1); 
                        break;
                    default:
                        oscillator.type = 'sine';
                        oscillator.frequency.setValueAtTime(440, audioContext.currentTime); 
                }
                
                gainNode.gain.setValueAtTime(0.3, audioContext.currentTime);
                gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.5);
                
                oscillator.start(audioContext.currentTime);
                oscillator.stop(audioContext.currentTime + 0.5);
            } catch (error) {
                console.log('Không thể phát âm thanh thông báo:', error);
            }
        }

        // Quản lý badge thông báo
        function updateNotificationBadge() {
            const tasks = loadTasksFromStorage();
            const now = new Date();
            const upcomingTasks = tasks.filter(task => 
                !task.completed && 
                new Date(task.dueDate) > now && 
                new Date(task.dueDate) <= new Date(now.getTime() + 24 * 60 * 60 * 1000)
            );
            
            const badge = document.getElementById('settingsBadge');
            if (upcomingTasks.length > 0) {
                badge.textContent = upcomingTasks.length;
                badge.style.display = 'flex';
            } else {
                badge.style.display = 'none';
            }
        }

        // Thông báo đến h hk
        function initStudyNotifications() {
            // Kiểm tra thông báo mỗi p
            studyNotificationInterval = setInterval(() => {
                checkUpcomingClasses();
                updateCurrentStudySession();
            }, 60000); // 1p

            // Kiểm tra ngay khi khởi động
            checkUpcomingClasses();
        }

        function checkUpcomingClasses() {
            if (!appSettings.notifications.enabled) return;

            const now = new Date();
            const timetable = loadTimetableFromStorage();
            const currentWeekKey = getWeekKey(currentWeek);
            
            let upcomingClasses = [];

            // Duyệt qua tất cả các ngày trong tuần hiện tại
            for (let day = 0; day < 7; day++) {
                const dayKey = `${currentWeekKey}-${day}`;
                if (timetable[dayKey]) {
                    Object.values(timetable[dayKey]).forEach(subject => {
                        const [startHour, startMinute] = subject.startTime.split(':').map(Number);
                        const classTime = new Date();
                        classTime.setHours(startHour, startMinute, 0, 0);
                        
                        // Tính thời gian chênh lệch (phút)
                        const timeDiff = (classTime - now) / (1000 * 60);
                        
                        // Nếu lớp học sắp diễn ra trong khoảng thời gian cài đặt
                        if (timeDiff > 0 && timeDiff <= appSettings.notifications.timeBefore) {
                            upcomingClasses.push({
                                subject: subject,
                                classTime: classTime,
                                timeDiff: timeDiff,
                                day: day
                            });
                        }
                    });
                }
            }

            // Sắp xếp theo thời gian gần nhất
            upcomingClasses.sort((a, b) => a.timeDiff - b.timeDiff);

            // Hiển thị thông báo cho môn sắp diễn ra
            upcomingClasses.forEach(classInfo => {
                if (!isClassNotifiedToday(classInfo)) {
                    showStudyNotification(classInfo);
                }
            });

            // Kiểm tra các môn học đã hoãn
            checkPostponedSessions();
        }

        function isClassNotifiedToday(classInfo) {
            const today = new Date().toDateString();
            const notifiedKey = `notified_${classInfo.subject.timetableId}_${today}`;
            return localStorage.getItem(notifiedKey) === 'true';
        }

        function markClassAsNotified(classInfo) {
            const today = new Date().toDateString();
            const notifiedKey = `notified_${classInfo.subject.timetableId}_${today}`;
            localStorage.setItem(notifiedKey, 'true');
        }

        function showStudyNotification(classInfo) {
            const timeRemaining = Math.floor(classInfo.timeDiff);
            const classTimeStr = classInfo.classTime.toLocaleTimeString('vi-VN', { 
                hour: '2-digit', 
                minute: '2-digit' 
            });

            const dayNames = ['Chủ nhật', 'Thứ 2', 'Thứ 3', 'Thứ 4', 'Thứ 5', 'Thứ 6', 'Thứ 7'];
            const dayName = dayNames[classInfo.day];

            const notificationMessage = `Môn: ${classInfo.subject.name}\nThời gian: ${classTimeStr} - ${classInfo.subject.endTime}\n${dayName}\n\nCòn ${timeRemaining} phút nữa là bắt đầu!`;

            // Hiển thị thông báo trên pc
            if (Notification.permission === "granted" && appSettings.notifications.desktopEnabled) {
                showDesktopNotification(
                    "📚 Đến giờ học!",
                    notificationMessage
                );
            }

            const notificationId = showNotification(
                "📚 Đến giờ học!",
                notificationMessage,
                "info",
                0
            );

            // Thêm nút chỉnh sửa cho thông báo
            const notification = document.getElementById(`notification-${notificationId}`);
            if (notification) {
                const actionsContainer = document.createElement('div');
                actionsContainer.className = 'study-actions';
                
                actionsContainer.innerHTML = `
                    <button class="study-action-btn postpone" onclick="postponeStudySession('${notificationId}', '${classInfo.subject.timetableId}')">
                        ⏸️ Hoãn 5 phút
                    </button>
                    <button class="study-action-btn start" onclick="startStudySession('${notificationId}', '${classInfo.subject.timetableId}')">
                        🎯 Bắt đầu học
                    </button>
                    <button class="study-action-btn skip" onclick="skipStudySession('${notificationId}', '${classInfo.subject.timetableId}')">
                        ❌ Bỏ qua
                    </button>
                `;
                
                notification.querySelector('.notification-content').appendChild(actionsContainer);
                notification.classList.add('study-notification');

                // Bộ đếm ngược
                const countdownElement = document.createElement('div');
                countdownElement.className = 'countdown-timer';
                countdownElement.id = `countdown-${notificationId}`;
                countdownElement.textContent = `⏰ ${timeRemaining} phút`;
                
                notification.querySelector('.notification-content').insertBefore(
                    countdownElement, 
                    notification.querySelector('.study-actions')
                );

                // Cập nhật bộ đếm ngược mỗi phút
                const countdownInterval = setInterval(() => {
                    const now = new Date();
                    const timeDiff = (classInfo.classTime - now) / (1000 * 60);
                    const remaining = Math.floor(timeDiff);
                    
                    if (remaining > 0) {
                        countdownElement.textContent = `⏰ ${remaining} phút`;
                    } else {
                        countdownElement.textContent = '🎯 Đã đến giờ học!';
                        clearInterval(countdownInterval);
                    }
                }, 60000);
            }

            markClassAsNotified(classInfo);
            return notificationId;
        }

        function postponeStudySession(notificationId, timetableId) {
            const postponedTime = new Date(Date.now() + 5 * 60 * 1000); // 5p
            postponedSessions.push({
                timetableId: timetableId,
                postponedUntil: postponedTime
            });

            showNotification("Đã hoãn", "Buổi học đã được hoãn 5 phút", "warning", 3000);
            closeNotification(notificationId);
        }

        function startStudySession(notificationId, timetableId) {
            const timetable = loadTimetableFromStorage();
            let subjectInfo = null;

            // Tìm thông tin môn học
            Object.values(timetable).forEach(daySchedule => {
                Object.values(daySchedule).forEach(subject => {
                    if (subject.timetableId === timetableId) {
                        subjectInfo = subject;
                    }
                });
            });

            if (subjectInfo) {
                currentStudySession = {
                    subject: subjectInfo,
                    startTime: new Date(),
                    timetableId: timetableId
                };
                studySessionStartTime = new Date();

                showNotification(
                    "Bắt đầu học!",
                    `Đã bắt đầu phiên học: ${subjectInfo.name}\nThời gian: ${subjectInfo.startTime} - ${subjectInfo.endTime}\nHãy tập trung học tập!`,
                    "success",
                    5000
                );

                // Hiển thị thông báo theo dõi thời gian học
                showStudyTimerNotification(subjectInfo);
            }

            closeNotification(notificationId);
        }

        function skipStudySession(notificationId, timetableId) {
            showNotification("Đã bỏ qua", "Buổi học đã được bỏ qua", "info", 3000);
            closeNotification(notificationId);
            
            // Đánh dấu là đã bỏ qua để không thông báo lại
            const today = new Date().toDateString();
            const skipKey = `skipped_${timetableId}_${today}`;
            localStorage.setItem(skipKey, 'true');
        }

        function showStudyTimerNotification(subjectInfo) {
            const notificationId = showNotification(
                "⏰ Đang học",
                `Môn: ${subjectInfo.name}\nĐã bắt đầu: ${studySessionStartTime.toLocaleTimeString('vi-VN')}\nThời lượng: ${Math.floor(subjectInfo.duration / 60)}h ${subjectInfo.duration % 60}p`,
                "info",
                0
            );

            const notification = document.getElementById(`notification-${notificationId}`);
            if (notification) {
                const timerElement = document.createElement('div');
                timerElement.className = 'countdown-timer';
                timerElement.id = `study-timer-${notificationId}`;
                timerElement.textContent = '🕐 00:00';
                
                notification.querySelector('.notification-content').appendChild(timerElement);

                const actionsContainer = document.createElement('div');
                actionsContainer.className = 'study-actions';
                
                actionsContainer.innerHTML = `
                    <button class="study-action-btn skip" onclick="endStudySession('${notificationId}', false)">
                        ❌ Kết thúc
                    </button>
                    <button class="study-action-btn start" onclick="endStudySession('${notificationId}', true)">
                        ✅ Hoàn thành
                    </button>
                `;
                
                notification.querySelector('.notification-content').appendChild(actionsContainer);

                // Cập nhật tg mỗi giây
                const timerInterval = setInterval(() => {
                    if (currentStudySession) {
                        const now = new Date();
                        const elapsed = Math.floor((now - studySessionStartTime) / 1000);
                        const minutes = Math.floor(elapsed / 60);
                        const seconds = elapsed % 60;
                        timerElement.textContent = `🕐 ${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
                    } else {
                        clearInterval(timerInterval);
                    }
                }, 1000);
            }
        }

        function endStudySession(notificationId, completed) {
            if (currentStudySession) {
                const endTime = new Date();
                const studyDuration = Math.floor((endTime - studySessionStartTime) / (1000 * 60)); // p

                if (completed) {
                    // Cập nhật vào thống kê
                    updateStudyStatistics(currentStudySession.subject, studyDuration);
                    
                    showNotification(
                        "Hoàn thành!",
                        `Đã hoàn thành phiên học: ${currentStudySession.subject.name}\nThời gian học: ${studyDuration} phút\nChúc mừng bạn! 🎉`,
                        "success",
                        5000
                    );
                } else {
                    showNotification(
                        "Đã kết thúc",
                        `Đã kết thúc phiên học: ${currentStudySession.subject.name}\nThời gian học: ${studyDuration} phút`,
                        "info",
                        3000
                    );
                }

                currentStudySession = null;
                studySessionStartTime = null;
            }

            closeNotification(notificationId);
        }

        function updateStudyStatistics(subject, duration) {
            const statsKey = 'studyStatistics';
            let statistics = JSON.parse(localStorage.getItem(statsKey)) || {};
            
            const today = new Date().toDateString();
            if (!statistics[today]) {
                statistics[today] = {};
            }
            
            if (!statistics[today][subject.name]) {
                statistics[today][subject.name] = 0;
            }
            
            statistics[today][subject.name] += duration;
            
            localStorage.setItem(statsKey, JSON.stringify(statistics));
            
            // Cập nhật task nếu có
            const tasks = loadTasksFromStorage();
            const updatedTasks = tasks.map(task => {
                if (task.name === subject.name && !task.completed) {
                    return {
                        ...task,
                        completed: true,
                        actualDuration: (task.actualDuration || 0) + duration
                    };
                }
                return task;
            });
            saveTasksToStorage(updatedTasks);
        }

        function checkPostponedSessions() {
            const now = new Date();
            postponedSessions = postponedSessions.filter(session => {
                if (now >= session.postponedUntil) {
                    // Hiển thị thông báo lại
                    const timetable = loadTimetableFromStorage();
                    Object.values(timetable).forEach(daySchedule => {
                        Object.values(daySchedule).forEach(subject => {
                            if (subject.timetableId === session.timetableId) {
                                showStudyNotification({
                                    subject: subject,
                                    classTime: new Date(now.getTime() + 2 * 60 * 1000), // 2 p nữa
                                    timeDiff: 2,
                                    day: new Date().getDay()
                                });
                            }
                        });
                    });
                    return false;
                }
                return true;
            });
        }

        function updateCurrentStudySession() {
            // Kiểm tra nếu đang trong phiên học
            if (currentStudySession && studySessionStartTime) {
                const now = new Date();
                const elapsed = (now - studySessionStartTime) / (1000 * 60); // p
                
                // Nếu vượt quá thời lượng dự kiến
                if (elapsed > currentStudySession.subject.duration) {
                    showNotification(
                        "Thời gian học",
                        `Phiên học ${currentStudySession.subject.name} đã vượt quá thời lượng dự kiến!\nHãy nghỉ ngơi một chút.`,
                        "warning",
                        5000
                    );
                }
            }
        }

        // Hiển thị lịch hk 
        function showTodaysSchedule() {
            const timetable = loadTimetableFromStorage();
            const currentWeekKey = getWeekKey(currentWeek);
            const today = new Date().getDay(); 
            const dayKey = `${currentWeekKey}-${today}`;
            
            let todaysClasses = [];
            
            if (timetable[dayKey]) {
                Object.values(timetable[dayKey]).forEach(subject => {
                    todaysClasses.push({
                        subject: subject,
                        time: `${subject.startTime} - ${subject.endTime}`
                    });
                });
            }
            
            // Sắp xếp theo thời gian
            todaysClasses.sort((a, b) => {
                const timeA = a.subject.startTime;
                const timeB = b.subject.startTime;
                return timeA.localeCompare(timeB);
            });
            
            let message = "📅 Lịch học hôm nay:\n\n";
            
            if (todaysClasses.length === 0) {
                message += "Hôm nay không có lịch học nào. Hãy tận dụng thời gian để ôn tập! 📚";
            } else {
                todaysClasses.forEach((classInfo, index) => {
                    message += `${index + 1}. ${classInfo.subject.name}\n   ⏰ ${classInfo.time}\n   📝 ${classInfo.subject.description || 'Không có mô tả'}\n\n`;
                });
                
                message += `Tổng cộng: ${todaysClasses.length} buổi học`;
            }
            
            showNotification("Lịch học hôm nay", message, "info", 15000);
        }

        // bảng setting
        function openSettings() {
            document.getElementById('settingsPanel').classList.add('open');
            document.getElementById('settingsOverlay').classList.add('show');
            loadSettingsToForm();
            updateStorageInfo();
        }

        function closeSettings() {
            document.getElementById('settingsPanel').classList.remove('open');
            document.getElementById('settingsOverlay').classList.remove('show');
            saveSettingsFromForm();
        }

        function loadSettingsToForm() {
            // thông báo
            document.getElementById('enableNotifications').checked = appSettings.notifications.enabled;
            document.getElementById('enableDesktopNotifications').checked = appSettings.notifications.desktopEnabled;
            document.getElementById('notificationTime').value = appSettings.notifications.timeBefore;
            document.getElementById('notificationSound').value = appSettings.notifications.sound;
            
            // giao diện
            document.getElementById('themeSelect').value = appSettings.appearance.theme;
            document.getElementById('languageSelect').value = appSettings.appearance.language;
            
            document.getElementById('trackStudyTime').checked = appSettings.study.trackStudyTime;
            document.getElementById('showProductivityTips').checked = appSettings.study.showProductivityTips;
            document.getElementById('studyGoal').value = appSettings.study.dailyGoal;
            document.getElementById('autoSync').checked = appSettings.study.autoSync;
            
            // cài đặt nâng cao
            document.getElementById('enableDebugMode').checked = appSettings.advanced.debugMode;
            document.getElementById('dataRetention').value = appSettings.advanced.dataRetention;
            
            updateNotificationHistory();
        }

        function saveSettingsFromForm() {
            // Lưu cài đặt thông báo
            appSettings.notifications.enabled = document.getElementById('enableNotifications').checked;
            appSettings.notifications.desktopEnabled = document.getElementById('enableDesktopNotifications').checked;
            appSettings.notifications.timeBefore = parseInt(document.getElementById('notificationTime').value);
            appSettings.notifications.sound = document.getElementById('notificationSound').value;
            
            // Lưu cài đặt giao diện
            appSettings.appearance.theme = document.getElementById('themeSelect').value;
            appSettings.appearance.language = document.getElementById('languageSelect').value;
            
            appSettings.study.trackStudyTime = document.getElementById('trackStudyTime').checked;
            appSettings.study.showProductivityTips = document.getElementById('showProductivityTips').checked;
            appSettings.study.dailyGoal = parseInt(document.getElementById('studyGoal').value);
            appSettings.study.autoSync = document.getElementById('autoSync').checked;
            
            // Lưu cài đặt nâng cao
            appSettings.advanced.debugMode = document.getElementById('enableDebugMode').checked;
            appSettings.advanced.dataRetention = parseInt(document.getElementById('dataRetention').value);
            
            saveAppSettings(appSettings);
            applySettings();
            
            showNotification("Cài đặt", "Đã lưu cài đặt thành công", "success");
        }

        function applySettings() {
            document.body.setAttribute('data-theme', appSettings.appearance.theme);
        }

        function updateStorageInfo() {
            let totalSize = 0;
            for (let key in localStorage) {
                if (localStorage.hasOwnProperty(key)) {
                    totalSize += localStorage[key].length * 2;
                }
            }
            
            const tasks = loadTasksFromStorage();
            const totalStudyTime = tasks.reduce((total, task) => total + (task.completed ? task.duration : 0), 0);
            const studyHours = (totalStudyTime / 60).toFixed(1);
            
            document.getElementById('storageUsage').textContent = (totalSize / 1024).toFixed(2) + ' KB';
            document.getElementById('totalSubjectsCount').textContent = tasks.length;
            document.getElementById('totalStudyHours').textContent = studyHours + ' giờ';
        }

        function testNotification() {
            // Test thông báo
            showNotification(
                "Kiểm tra thông báo",
                "Đây là thông báo kiểm tra từ hệ thống cài đặt",
                "info",
                5000
            );
            
            // Test thông báo pc 
            if (Notification.permission === "granted" && appSettings.notifications.desktopEnabled) {
                showDesktopNotification(
                    "Kiểm tra Desktop Notification",
                    "Đây là thông báo desktop từ ứng dụng quản lý học tập"
                );
            } else if (appSettings.notifications.desktopEnabled) {
                showNotification(
                    "Thông báo Desktop",
                    "Vui lòng cấp quyền thông báo để nhận thông báo trên desktop",
                    "warning",
                    5000
                );
            }
        }

        function exportData() {
            const data = {
                tasks: loadTasksFromStorage(),
                timetable: loadTimetableFromStorage(),
                settings: appSettings,
                exportDate: new Date().toISOString()
            };
            
            const dataStr = JSON.stringify(data, null, 2);
            const dataBlob = new Blob([dataStr], {type: 'application/json'});
            
            const link = document.createElement('a');
            link.href = URL.createObjectURL(dataBlob);
            link.download = `study_data_${new Date().toISOString().split('T')[0]}.json`;
            link.click();
            
            showNotification("Xuất dữ liệu", "Đã xuất dữ liệu thành công", "success");
        }

        function clearAllData() {
            if (confirm('Bạn có chắc chắn muốn xóa TẤT CẢ dữ liệu? Hành động này không thể hoàn tác!')) {
                localStorage.clear();
                showNotification("Xóa dữ liệu", "Đã xóa tất cả dữ liệu", "info");
                setTimeout(() => {
                    location.reload();
                }, 2000);
            }
        }

        function updateNotificationHistory() {
            const historyContainer = document.getElementById('notificationHistory');
            historyContainer.innerHTML = `
                <div style="padding: 8px; margin-bottom: 5px; background: white; border-radius: 4px; border-left: 3px solid #4a6fa5">
                    <div style="font-weight: 600; font-size: 0.9rem;">Hệ thống đã sẵn sàng</div>
                    <div style="font-size: 0.8rem; color: #666;">Tất cả tính năng đã được kích hoạt</div>
                    <div style="font-size: 0.7rem; color: #999;">${new Date().toLocaleString('vi-VN')}</div>
                </div>
            `;
        }

        // THỐNG KÊ CHI TIẾT
        function showStatsDetails(defaultTab = 'subjects') {
            const modal = document.getElementById('statsModal');
            modal.style.display = 'flex';
            
            switchStatsTab(defaultTab);
            updateDetailedStats();
        }

        function closeStatsModal() {
            document.getElementById('statsModal').style.display = 'none';
        }

        function setupStatsTabs() {
            document.querySelectorAll('.stats-tab').forEach(tab => {
                tab.addEventListener('click', function() {
                    const tabName = this.getAttribute('data-tab');
                    switchStatsTab(tabName);
                });
            });
        }

        function switchStatsTab(tabName) {
            // Ẩn tất cả các tab và nội dung
            document.querySelectorAll('.stats-tab').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.stats-content').forEach(content => content.classList.remove('active'));
            
            // Hiển thị tab được chọn
            const selectedTab = document.querySelector(`.stats-tab[data-tab="${tabName}"]`);
            const selectedContent = document.getElementById(`${tabName}-stats`);
            
            if (selectedTab && selectedContent) {
                selectedTab.classList.add('active');
                selectedContent.classList.add('active');
                
                // Cập nhật dữ liệu cho tab được chọn
                updateDetailedStatsForTab(tabName);
            }
        }

        function updateDetailedStatsForTab(tabName) {
            switch(tabName) {
                case 'subjects':
                    updateSubjectStats();
                    break;
                case 'days':
                    updateDayStats();
                    break;
                case 'completion':
                    updateCompletionStats();
                    break;
                case 'performance':
                    updatePerformanceStats();
                    break;
            }
        }

        function updateDetailedStats() {
            updateSubjectStats();
            updateDayStats();
            updateCompletionStats();
            updatePerformanceStats();
        }

        function updateSubjectStats() {
            const tasks = loadTasksFromStorage();
            const timetable = loadTimetableFromStorage();
            const container = document.getElementById('subjectStatsList');
            
            if (tasks.length === 0) {
                container.innerHTML = '<div class="empty-state"><p>Chưa có dữ liệu thống kê</p></div>';
                return;
            }
            
            const subjectStats = {};
            
            tasks.forEach(task => {
                if (!subjectStats[task.name]) {
                    subjectStats[task.name] = {
                        totalTime: 0,
                        completed: task.completed,
                        priority: task.priority,
                        days: new Set(),
                        sessions: 0
                    };
                }
                
                subjectStats[task.name].totalTime += task.duration;
                subjectStats[task.name].sessions++;

                Object.values(timetable).forEach(daySchedule => {
                    Object.values(daySchedule).forEach(subject => {
                        if (subject.id === task.id) {
                            subjectStats[task.name].days.add(subject.startTime.split(':')[0] + 'h');
                        }
                    });
                });
            });
            
            container.innerHTML = '';
            
            Object.entries(subjectStats).forEach(([subjectName, stats]) => {
                const statItem = document.createElement('div');
                statItem.className = 'subject-stat-item';
                
                const hours = Math.floor(stats.totalTime / 60);
                const minutes = stats.totalTime % 60;
                const timeText = hours > 0 ? `${hours}h ${minutes}p` : `${minutes}p`;
                const daysText = Array.from(stats.days).join(', ') || 'Chưa có lịch học';
                const completionRate = stats.sessions > 0 ? Math.round((stats.completed ? 1 : 0) * 100) : 0;
                
                statItem.innerHTML = `
                    <div class="subject-stat-header">
                        <div class="subject-name">${subjectName}</div>
                        <div class="subject-total-time">${timeText}</div>
                    </div>
                    <div class="task-meta">
                        <span>📅 ${daysText}</span> | 
                        <span>📊 ${stats.sessions} buổi học</span> | 
                        <span>🎯 ${completionRate}% hoàn thành</span> | 
                        <span>⚡ ${getPriorityText(stats.priority)}</span>
                    </div>
                    <div class="progress-bar" style="margin-top: 8px;">
                        <div class="progress" style="width: ${completionRate}%"></div>
                    </div>
                `;
                
                container.appendChild(statItem);
            });
        }

        function updateDayStats() {
            const timetable = loadTimetableFromStorage();
            const tasks = loadTasksFromStorage();
            const container = document.getElementById('dayStatsGrid');
            
            const dayStats = {
                0: { name: 'Chủ nhật', totalTime: 0, subjectCount: 0, completed: 0 },
                1: { name: 'Thứ 2', totalTime: 0, subjectCount: 0, completed: 0 },
                2: { name: 'Thứ 3', totalTime: 0, subjectCount: 0, completed: 0 },
                3: { name: 'Thứ 4', totalTime: 0, subjectCount: 0, completed: 0 },
                4: { name: 'Thứ 5', totalTime: 0, subjectCount: 0, completed: 0 },
                5: { name: 'Thứ 6', totalTime: 0, subjectCount: 0, completed: 0 },
                6: { name: 'Thứ 7', totalTime: 0, subjectCount: 0, completed: 0 }
            };
            
            Object.entries(timetable).forEach(([dayKey, daySchedule]) => {
                const dayIndex = parseInt(dayKey.split('-')[1]);
                Object.values(daySchedule).forEach(subject => {
                    dayStats[dayIndex].totalTime += subject.duration || 60;
                    dayStats[dayIndex].subjectCount++;
                    
                    const task = tasks.find(t => t.id === subject.id);
                    if (task && task.completed) {
                        dayStats[dayIndex].completed++;
                    }
                });
            });
            
            container.innerHTML = '';
            
            Object.values(dayStats).forEach(day => {
                const hours = Math.floor(day.totalTime / 60);
                const minutes = day.totalTime % 60;
                const timeText = hours > 0 ? `${hours}h ${minutes}p` : `${minutes}p`;
                const completionRate = day.subjectCount > 0 ? Math.round((day.completed / day.subjectCount) * 100) : 0;
                
                const statItem = document.createElement('div');
                statItem.className = 'day-stat-item';
                statItem.innerHTML = `
                    <div class="day-name">${day.name}</div>
                    <div class="day-study-time">${timeText}</div>
                    <div class="day-subject-count">${day.subjectCount} môn học</div>
                    <div class="progress-bar" style="margin-top: 8px; height: 6px;">
                        <div class="progress" style="width: ${completionRate}%"></div>
                    </div>
                    <div style="font-size: 0.8rem; color: #666; margin-top: 5px;">${completionRate}% hoàn thành</div>
                `;
                
                container.appendChild(statItem);
            });
        }

        function updateCompletionStats() {
            const tasks = loadTasksFromStorage();
            const container = document.getElementById('completionProgress');
            
            if (tasks.length === 0) {
                container.innerHTML = '<div class="empty-state"><p>Chưa có dữ liệu thống kê</p></div>';
                return;
            }
            
            container.innerHTML = '';
            
            tasks.forEach(task => {
                const progressItem = document.createElement('div');
                progressItem.className = 'progress-item';
                
                const completionPercent = task.completed ? 100 : 0;
                const timeSpent = task.completed ? task.duration : 0;
                const hours = Math.floor(timeSpent / 60);
                const minutes = timeSpent % 60;
                const timeText = hours > 0 ? `${hours}h ${minutes}p` : `${minutes}p`;
                
                progressItem.innerHTML = `
                    <div class="progress-subject">
                        <div>${task.name}</div>
                        <small style="color: #666;">${timeText}</small>
                    </div>
                    <div class="progress-bar-small">
                        <div class="progress-small" style="width: ${completionPercent}%"></div>
                    </div>
                    <div class="progress-percent">${completionPercent}%</div>
                `;
                
                container.appendChild(progressItem);
            });
        }

        function updatePerformanceStats() {
            const tasks = loadTasksFromStorage();
            const timetable = loadTimetableFromStorage();
            
            // Tính thời gian học trung bình mỗi ngày
            let totalStudyTime = 0;
            let studyDays = new Set();
            
            Object.entries(timetable).forEach(([dayKey, daySchedule]) => {
                Object.values(daySchedule).forEach(subject => {
                    totalStudyTime += subject.duration || 60;
                    studyDays.add(dayKey.split('-')[0]);
                });
            });
            
            const avgStudyTimePerDay = studyDays.size > 0 ? totalStudyTime / studyDays.size : 0;
            const avgHours = Math.floor(avgStudyTimePerDay / 60);
            const avgMinutes = Math.round(avgStudyTimePerDay % 60);
            
            const completedTasks = tasks.filter(task => task.completed).length;
            const totalTasks = tasks.length;
            const efficiencyScore = totalTasks > 0 ? Math.round((completedTasks / totalTasks) * 100) : 0;
            
            const consistencyScore = Math.min(100, Math.round((studyDays.size / 7) * 100));
            
            let focusTime = 0;
            tasks.forEach(task => {
                if (task.priority === 'high' && task.completed) {
                    focusTime += task.duration;
                }
            });
            const focusHours = Math.floor(focusTime / 60);
            const focusMinutes = focusTime % 60;
            
            // Update DOM
            document.getElementById('avgStudyTime').textContent = 
                avgHours > 0 ? `${avgHours}h ${avgMinutes}p` : `${avgMinutes}p`;
            document.getElementById('efficiencyScore').textContent = `${efficiencyScore}%`;
            document.getElementById('consistencyScore').textContent = `${consistencyScore}%`;
            document.getElementById('focusTime').textContent = 
                focusHours > 0 ? `${focusHours}h ${focusMinutes}p` : `${focusMinutes}p`;
            
            // Phân tích hiệu suất
            const analysisContainer = document.getElementById('performanceAnalysis');
            let analysisHTML = '';
            
            if (totalTasks === 0) {
                analysisHTML = '<p>Chưa có đủ dữ liệu để phân tích hiệu suất học tập.</p>';
            } else {
                const completionRate = Math.round((completedTasks / totalTasks) * 100);
                
                analysisHTML = `
                    <div style="margin-bottom: 15px;">
                        <h4>📊 Tổng quan Hiệu suất</h4>
                        <p>Tỷ lệ hoàn thành: <strong>${completionRate}%</strong></p>
                        <p>Ngày học trung bình/tuần: <strong>${studyDays.size}</strong> ngày</p>
                        <p>Thời gian tập trung cao: <strong>${focusHours > 0 ? `${focusHours}h ${focusMinutes}p` : `${focusMinutes}p`}</strong></p>
                    </div>
                `;
                
                if (completionRate >= 80) {
                    analysisHTML += `<p style="color: var(--success-color);">🎉 Xuất sắc! Bạn đang duy trì hiệu suất học tập rất tốt.</p>`;
                } else if (completionRate >= 60) {
                    analysisHTML += `<p style="color: var(--warning-color);">👍 Tốt! Hãy tiếp tục duy trì và cải thiện hơn nữa.</p>`;
                } else {
                    analysisHTML += `<p style="color: var(--danger-color);">💡 Cần cải thiện! Hãy tập trung vào việc hoàn thành các môn học quan trọng.</p>`;
                }
                
                if (studyDays.size < 3) {
                    analysisHTML += `<p style="color: var(--warning-color);">📅 Gợi ý: Hãy cố gắng học đều đặn hơn, ít nhất 3-4 ngày/tuần.</p>`;
                }
            }
            
            analysisContainer.innerHTML = analysisHTML;
        }

        function getPriorityText(priority) {
            const priorityTexts = {
                'low': 'Thấp',
                'medium': 'Trung bình',
                'high': 'Cao'
            };
            return priorityTexts[priority] || 'Trung bình';
        }

        // Quản lý nhiệm vụ
        function addTask(event) {
            event.preventDefault();
            
            const name = document.getElementById('taskName').value;
            const description = document.getElementById('taskDescription').value;
            const dueDate = document.getElementById('taskDueDate').value;
            const priority = document.getElementById('taskPriority').value;
            const duration = parseInt(document.getElementById('taskDuration').value);
            
            const newTask = {
                id: generateId(),
                name,
                description,
                dueDate,
                priority,
                duration,
                completed: false,
                createdAt: new Date().toISOString(),
                inTimetable: false,
                fromTimetable: false
            };
            
            const tasks = loadTasksFromStorage();
            tasks.push(newTask);
            saveTasksToStorage(tasks);
            
            renderTasks();
            updateStats();
            updateNotificationBadge();
            
            showNotification("Thành công", `Đã thêm môn học "${name}"`, "success");
            
            document.getElementById('taskForm').reset();
        }

        function deleteTask(taskId) {
            if (confirm('Bạn có chắc chắn muốn xóa môn học này?')) {
                const tasks = loadTasksFromStorage();
                const taskToDelete = tasks.find(task => task.id === taskId);
                const updatedTasks = tasks.filter(task => task.id !== taskId);
                saveTasksToStorage(updatedTasks);
                
                renderTasks();
                updateStats();
                updateNotificationBadge();
                
                showNotification("Đã xóa", `Đã xóa môn học "${taskToDelete.name}"`, "info");
            }
        }

        function toggleTaskCompletion(taskId) {
            const tasks = loadTasksFromStorage();
            const updatedTasks = tasks.map(task => {
                if (task.id === taskId) {
                    const newCompletedState = !task.completed;
                    if (newCompletedState) {
                        showNotification("Hoàn thành", `Đã hoàn thành môn học "${task.name}"`, "success");
                    }
                    return { ...task, completed: newCompletedState };
                }
                return task;
            });
            saveTasksToStorage(updatedTasks);
            renderTasks();
            updateStats();
            updateNotificationBadge();
        }

        function renderTasks() {
            const taskList = document.getElementById('taskList');
            const tasks = loadTasksFromStorage();
            
            if (tasks.length === 0) {
                taskList.innerHTML = `
                    <div class="empty-state">
                        <i>📚</i>
                        <p>Chưa có môn học nào. Hãy thêm môn học đầu tiên!</p>
                    </div>
                `;
                return;
            }
            
            taskList.innerHTML = '';
            
            tasks.forEach(task => {
                const taskElement = document.createElement('div');
                taskElement.className = `task-item ${task.completed ? 'completed' : ''} priority-${task.priority}`;
                
                if (!task.completed && new Date(task.dueDate) < new Date()) {
                    taskElement.classList.add('overdue');
                }
                
                const timetableIndicator = task.inTimetable ? 
                    '<span class="timetable-indicator" title="Đã có trong thời khóa biểu">📅</span>' : '';
                
                const timetableButton = task.inTimetable ? 
                    '<button class="btn-primary" disabled>✓ Đã thêm</button>' :
                    `<button class="btn-primary" onclick="quickAddToTimetable('${task.id}')">+ TKB</button>`;
                
                taskElement.innerHTML = `
                    <div class="task-info">
                        <h3>${task.name} ${timetableIndicator}</h3>
                        <p>${task.description || 'Không có mô tả'}</p>
                        <div class="task-meta">
                            <span>⏰ ${formatDateTime(task.dueDate)}</span> | 
                            <span>⏱️ ${task.duration} phút</span> | 
                            <span>${getTimeRemaining(task.dueDate)}</span>
                            ${task.fromTimetable ? '<span style="color: #4a6fa5; margin-left: 8px;">(Từ TKB)</span>' : ''}
                        </div>
                    </div>
                    <div class="task-actions">
                        <button class="${task.completed ? 'btn-warning' : 'btn-success'}" onclick="toggleTaskCompletion('${task.id}')">
                            ${task.completed ? '↶' : '✓'}
                        </button>
                        ${timetableButton}
                        <button class="btn-danger" onclick="deleteTask('${task.id}')">✕</button>
                    </div>
                `;
                
                taskList.appendChild(taskElement);
            });
            
            renderUpcomingTasks();
            populateTimetableSubjects();
        }

        function renderUpcomingTasks() {
            const upcomingTasksContainer = document.getElementById('upcomingTasks');
            const tasks = loadTasksFromStorage();
            const now = new Date();
            const next24Hours = new Date(now.getTime() + 24 * 60 * 60 * 1000);
            
            const upcomingTasks = tasks
                .filter(task => !task.completed && new Date(task.dueDate) > now && new Date(task.dueDate) <= next24Hours)
                .sort((a, b) => new Date(a.dueDate) - new Date(b.dueDate))
                .slice(0, 5);
            
            if (upcomingTasks.length === 0) {
                upcomingTasksContainer.innerHTML = `
                    <div class="empty-state">
                        <i>⏰</i>
                        <p>Không có môn học nào sắp đến hạn</p>
                    </div>
                `;
                return;
            }
            
            upcomingTasksContainer.innerHTML = '';
            
            upcomingTasks.forEach(task => {
                const taskElement = document.createElement('div');
                taskElement.className = `task-item priority-${task.priority}`;
                
                taskElement.innerHTML = `
                    <div class="task-info">
                        <h3>${task.name}</h3>
                        <div class="task-meta">
                            <span>⏰ ${formatDateTime(task.dueDate)}</span> | 
                            <span>⏱️ ${task.duration} phút</span>
                        </div>
                    </div>
                `;
                
                upcomingTasksContainer.appendChild(taskElement);
            });
        }

        function updateStats() {
            const tasks = loadTasksFromStorage();
            const totalTasks = tasks.length;
            const completedTasks = tasks.filter(task => task.completed).length;
            const pendingTasks = totalTasks - completedTasks;
            
            const totalStudyTime = tasks.reduce((total, task) => {
                return total + (task.completed ? task.duration : 0);
            }, 0);
            
            const studyHours = Math.floor(totalStudyTime / 60);
            const studyMinutes = totalStudyTime % 60;
            const studyTimeText = studyHours > 0 ? `${studyHours}h ${studyMinutes}p` : `${studyMinutes}p`;
            
            const completionPercentage = totalTasks > 0 ? Math.round((completedTasks / totalTasks) * 100) : 0;
            
            document.getElementById('totalTasks').textContent = totalTasks;
            document.getElementById('completedTasks').textContent = completedTasks;
            document.getElementById('pendingTasks').textContent = pendingTasks;
            document.getElementById('studyTime').textContent = studyTimeText;
            document.getElementById('progressBar').style.width = `${completionPercentage}%`;
            document.getElementById('progressText').textContent = `${completionPercentage}% hoàn thành`;
        }

        // chức năng lịch trình
        function calculateDuration(startTime, endTime) {
            const start = new Date(`2000-01-01T${startTime}`);
            const end = new Date(`2000-01-01T${endTime}`);
            
            if (end <= start) {
                return { hours: 0, minutes: 0, totalMinutes: 0 };
            }
            
            const diffMs = end - start;
            const totalMinutes = Math.floor(diffMs / (1000 * 60));
            const hours = Math.floor(totalMinutes / 60);
            const minutes = totalMinutes % 60;
            
            return { hours, minutes, totalMinutes };
        }

        function getWeekKey(weekOffset) {
            const now = new Date();
            const startOfWeek = new Date(now);
            startOfWeek.setDate(now.getDate() - now.getDay() + 1 + (weekOffset * 7));
            return startOfWeek.toISOString().split('T')[0];
        }

        function updateWeekDisplay() {
            const now = new Date();
            const startOfWeek = new Date(now);
            startOfWeek.setDate(now.getDate() - now.getDay() + 1 + (currentWeek * 7));
            
            const endOfWeek = new Date(startOfWeek);
            endOfWeek.setDate(startOfWeek.getDate() + 6);
            
            const options = { day: 'numeric', month: 'numeric' };
            const startStr = startOfWeek.toLocaleDateString('vi-VN', options);
            const endStr = endOfWeek.toLocaleDateString('vi-VN', options);
            
            document.getElementById('currentWeek').textContent = `Tuần ${startStr} - ${endStr}`;
        }

        function generateTimetable() {
            const timetableBody = document.getElementById('timetableBody');
            timetableBody.innerHTML = '';
            
            const timePeriods = [
                { name: 'SÁNG', start: 3, end: 12, class: 'morning-period' },
                { name: 'CHIỀU', start: 13, end: 18, class: 'afternoon-period' },
                { name: 'TỐI', start: 19, end: 23, class: 'evening-period' }
            ];
            
            const timetable = loadTimetableFromStorage();
            const weekKey = getWeekKey(currentWeek);
            
            timePeriods.forEach(period => {
                for (let hour = period.start; hour <= period.end; hour++) {
                    const row = document.createElement('tr');
                    
                    // Ô hiển thị khung giờ
                    const periodCell = document.createElement('td');
                    periodCell.className = `time-period-column ${period.class}`;
                    if (hour === period.start) {
                        periodCell.rowSpan = period.end - period.start + 1;
                        periodCell.textContent = period.name;
                    } else {
                        periodCell.style.display = 'none';
                    }
                    row.appendChild(periodCell);
                    
                    // Ô hiển thị giờ
                    const timeCell = document.createElement('td');
                    timeCell.className = 'time-slot';
                    timeCell.innerHTML = `<strong>${hour.toString().padStart(2, '0')}:00</strong>`;
                    row.appendChild(timeCell);
                    
                    // Tạo ô cho mỗi ngày trong tuần
                    for (let day = 1; day <= 7; day++) {
                        const dayIndex = day === 7 ? 0 : day;
                        const cell = document.createElement('td');
                        cell.dataset.day = dayIndex;
                        cell.dataset.hour = hour;
                        
                        cell.addEventListener('click', () => openTimetableModal(dayIndex, hour));
                        
                        const dayKey = `${weekKey}-${dayIndex}`;
                        
                        if (timetable[dayKey]) {
                            const daySchedule = timetable[dayKey];
                            const currentHourStart = hour * 60;
                            const currentHourEnd = (hour + 1) * 60;
                            
                            // Tìm tất cả môn học diễn ra trong giờ hiện tại
                            const subjectsThisHour = [];
                            
                            Object.values(daySchedule).forEach(subject => {
                                const subjectStart = parseInt(subject.startTime.split(':')[0]) * 60 + 
                                                   parseInt(subject.startTime.split(':')[1]);
                                const subjectEnd = parseInt(subject.endTime.split(':')[0]) * 60 + 
                                                 parseInt(subject.endTime.split(':')[1]);
                                
                                // Kiểm tra xem môn học có diễn ra trong giờ hiện tại không
                                if (subjectStart < currentHourEnd && subjectEnd > currentHourStart) {
                                    subjectsThisHour.push({
                                        subject: subject,
                                        startMinutes: subjectStart,
                                        endMinutes: subjectEnd
                                    });
                                }
                            });
                            
                            // Sắp xếp môn học theo thời gian bắt đầu
                            subjectsThisHour.sort((a, b) => a.startMinutes - b.startMinutes);
                            
                            // Hiển thị tất cả môn học VỚI THỜI GIAN ĐẦY ĐỦ
                            subjectsThisHour.forEach(({ subject, startMinutes }) => {
                                const subjectElement = document.createElement('div');
                                subjectElement.className = `timetable-subject ${subject.priority}`;
                                subjectElement.style.backgroundColor = subject.color;
                                subjectElement.style.marginBottom = '2px';
                                subjectElement.style.fontSize = '0.7rem';
                                subjectElement.style.padding = '2px 4px';
                                subjectElement.style.borderRadius = '2px';
                                subjectElement.style.cursor = 'pointer';
                                
                                let subjectText = subject.name;
                                if (subject.note) {
                                    subjectText += ' 📝';
                                }
                                
                                // hiển thị tg cho môn hk
                                const endTimeDisplay = subject.endTime;
                                subjectElement.textContent = `${subjectText} (${subject.startTime}-${endTimeDisplay})`;
                                
                                let tooltipText = `${subject.name}\n${subject.description || 'Không có mô tả'}\n${subject.startTime}-${subject.endTime}`;
                                if (subject.note) {
                                    tooltipText += `\n\nGhi chú: ${subject.note}`;
                                }
                                tooltipText += `\nThời lượng: ${Math.floor(subject.duration / 60)}h ${subject.duration % 60}p`;
                                subjectElement.title = tooltipText;
                                
                                // chỉnh sửa
                                subjectElement.addEventListener('click', (e) => {
                                    e.stopPropagation();
                                    editTimetableSubject(dayIndex, subject.timetableId, weekKey);
                                });
                                
                                // xóa 
                                subjectElement.addEventListener('contextmenu', (e) => {
                                    e.preventDefault();
                                    removeFromTimetable(dayIndex, subject.timetableId, weekKey);
                                });
                                
                                cell.appendChild(subjectElement);
                            });
                        }
                        
                        row.appendChild(cell);
                    }
                    
                    timetableBody.appendChild(row);
                }
            });
        }

        function generateDetailedTimetable() {
            const timetableBody = document.getElementById('timetableBody');
            timetableBody.innerHTML = '';
            
            document.getElementById('timetable').classList.add('timetable-detailed');
            
            const timePeriods = [
                { name: 'SÁNG', start: 3, end: 12, class: 'morning-period' },
                { name: 'CHIỀU', start: 13, end: 18, class: 'afternoon-period' },
                { name: 'TỐI', start: 19, end: 23, class: 'evening-period' }
            ];
            
            const timetable = loadTimetableFromStorage();
            const weekKey = getWeekKey(currentWeek);
            
            timePeriods.forEach(period => {
                for (let hour = period.start; hour <= period.end; hour++) {
                    for (let minuteSlot = 0; minuteSlot < 2; minuteSlot++) {
                        const row = document.createElement('tr');
                        const minutes = minuteSlot === 0 ? '00' : '30';
                        const currentTime = hour * 60 + (minuteSlot === 0 ? 0 : 30);
                        
                        // Ô hiển thị khung giờ
                        if (hour === period.start && minuteSlot === 0) {
                            const periodCell = document.createElement('td');
                            periodCell.className = `time-period-column ${period.class}`;
                            periodCell.rowSpan = (period.end - period.start + 1) * 2;
                            periodCell.textContent = period.name;
                            row.appendChild(periodCell);
                        } else if (hour === period.start && minuteSlot === 1) {
                            // Không thêm periodCell cho dòng thứ 2 của giờ đầu tiên
                        } else if (minuteSlot === 0) {
                            const periodCell = document.createElement('td');
                            periodCell.className = `time-period-column ${period.class}`;
                            periodCell.style.display = 'none';
                            row.appendChild(periodCell);
                        }
                        
                        // Ô hiển thị giờ
                        const timeCell = document.createElement('td');
                        timeCell.className = 'time-slot-small';
                        timeCell.innerHTML = `<strong>${hour.toString().padStart(2, '0')}:${minutes}</strong>`;
                        row.appendChild(timeCell);
                        
                        // Tạo ô cho mỗi ngày trong tuần
                        for (let day = 1; day <= 7; day++) {
                            const dayIndex = day === 7 ? 0 : day;
                            const cell = document.createElement('td');
                            cell.dataset.day = dayIndex;
                            cell.dataset.hour = hour;
                            cell.dataset.minute = minutes;
                            
                            cell.addEventListener('click', () => openTimetableModal(dayIndex, hour, minuteSlot === 0 ? 0 : 30));
                            
                            const dayKey = `${weekKey}-${dayIndex}`;
                            
                            if (timetable[dayKey]) {
                                const daySchedule = timetable[dayKey];
                                const currentSlotStart = currentTime;
                                const currentSlotEnd = currentTime + 30;
                                
                                // Tìm tất cả môn học diễn ra trong khung giờ hiện tại
                                const subjectsThisSlot = [];
                                
                                Object.values(daySchedule).forEach(subject => {
                                    const subjectStart = parseInt(subject.startTime.split(':')[0]) * 60 + 
                                                       parseInt(subject.startTime.split(':')[1]);
                                    const subjectEnd = parseInt(subject.endTime.split(':')[0]) * 60 + 
                                                     parseInt(subject.endTime.split(':')[1]);
                                    
                                    // Kiểm tra xem môn học có diễn ra trong khung giờ hiện tại không
                                    if (subjectStart < currentSlotEnd && subjectEnd > currentSlotStart) {
                                        subjectsThisSlot.push({
                                            subject: subject,
                                            startMinutes: subjectStart
                                        });
                                    }
                                });
                                
                                // Sắp xếp môn học theo thời gian bắt đầu
                                subjectsThisSlot.sort((a, b) => a.startMinutes - b.startMinutes);
                                
                                // Hiển thị tất cả môn học VỚI THỜI GIAN ĐẦY ĐỦ
                                subjectsThisSlot.forEach(({ subject, startMinutes }) => {
                                    const subjectElement = document.createElement('div');
                                    subjectElement.className = `timetable-subject timetable-subject-small ${subject.priority}`;
                                    subjectElement.style.backgroundColor = subject.color;
                                    subjectElement.style.marginBottom = '1px';
                                    subjectElement.style.fontSize = '0.6rem';
                                    subjectElement.style.padding = '1px 2px';
                                    subjectElement.style.borderRadius = '1px';
                                    subjectElement.style.cursor = 'pointer';
                                    
                                    let subjectText = subject.name;
                                    if (subject.note) {
                                        subjectText += ' 📝';
                                    }
                                    
                                    // Hiển thị tg cho các môn hk
                                    subjectElement.textContent = `${subjectText} (${subject.startTime}-${subject.endTime})`;
                                    
                                    // Tooltip với thông tin đầy đủ
                                    let tooltipText = `${subject.name}\n${subject.description || 'Không có mô tả'}\n${subject.startTime}-${subject.endTime}`;
                                    if (subject.note) {
                                        tooltipText += `\n\nGhi chú: ${subject.note}`;
                                    }
                                    tooltipText += `\nThời lượng: ${Math.floor(subject.duration / 60)}h ${subject.duration % 60}p`;
                                    subjectElement.title = tooltipText;
                                    
                                    // chỉnh sửa môn hk
                                    subjectElement.addEventListener('click', (e) => {
                                        e.stopPropagation();
                                        editTimetableSubject(dayIndex, subject.timetableId, weekKey);
                                    });
                                    
                                    // xóa môn hk
                                    subjectElement.addEventListener('contextmenu', (e) => {
                                        e.preventDefault();
                                        removeFromTimetable(dayIndex, subject.timetableId, weekKey);
                                    });
                                    
                                    cell.appendChild(subjectElement);
                                });
                            }
                            
                            row.appendChild(cell);
                        }
                        
                        timetableBody.appendChild(row);
                    }
                }
            });
        }

        function toggleTimetableView() {
            isDetailedView = !isDetailedView;
            const toggleButton = document.getElementById('toggleView');
            
            if (isDetailedView) {
                toggleButton.textContent = '📋 Xem thường';
                generateDetailedTimetable();
            } else {
                toggleButton.textContent = '📊 Xem chi tiết';
                document.getElementById('timetable').classList.remove('timetable-detailed');
                generateTimetable();
            }
        }

        //  Chỉnh sửa môn học trong TKB
        function editTimetableSubject(day, timetableId, weekKey) {
            const timetable = loadTimetableFromStorage();
            const dayKey = `${weekKey}-${day}`;
            
            if (timetable[dayKey] && timetable[dayKey][timetableId]) {
                const subject = timetable[dayKey][timetableId];
                
                // Đặt chế độ chỉnh sửa
                document.getElementById('editMode').value = 'true';
                document.getElementById('editTimetableId').value = timetableId;
                document.getElementById('editDay').value = day;
                document.getElementById('editWeekKey').value = weekKey;
                
                // Đặt tiêu đề modal
                document.getElementById('timetableModalTitle').textContent = 'Chỉnh sửa môn học';
                
                // Điền thông tin vào form
                document.getElementById('timetableSubject').value = subject.id;
                document.getElementById('subjectDescription').value = subject.description || '';
                document.getElementById('timetableDay').value = day;
                document.getElementById('subjectPriority').value = subject.priority;
                document.getElementById('timetableColor').value = subject.color;
                document.getElementById('timetableNote').value = subject.note || '';
                
                // Đặt thời gian
                const [startHour, startMinute] = subject.startTime.split(':').map(Number);
                const [endHour, endMinute] = subject.endTime.split(':').map(Number);
                
                startTime24h = subject.startTime;
                endTime24h = subject.endTime;
                
                initializeTimeDropdowns();
                
                // Hiển thị ghi chú nếu có
                if (subject.note) {
                    document.getElementById('noteContent').classList.add('show');
                    document.getElementById('notePreview').classList.add('show');
                    document.getElementById('notePreviewText').textContent = subject.note;
                    document.getElementById('noteToggle').textContent = '- Ẩn ghi chú';
                } else {
                    document.getElementById('noteContent').classList.remove('show');
                    document.getElementById('notePreview').classList.remove('show');
                    document.getElementById('noteToggle').textContent = '+ Thêm ghi chú';
                }
                
                // Hiển thị nút chỉnh sửa
                document.getElementById('editActions').style.display = 'block';
                document.getElementById('submitTimetableBtn').textContent = 'Cập nhật';
                
                // Mở modal
                document.getElementById('timetableModal').style.display = 'flex';
                
                showNotification("Chỉnh sửa", `Đang chỉnh sửa môn học "${subject.name}"`, "info");
            }
        }

        function openTimetableModal(day, hour, minute = 0) {
            // Đặt chế độ thêm mới
            document.getElementById('editMode').value = 'false';
            document.getElementById('editTimetableId').value = '';
            document.getElementById('editDay').value = '';
            document.getElementById('editWeekKey').value = '';
            
            // Đặt tiêu đề modal
            document.getElementById('timetableModalTitle').textContent = 'Thêm môn học vào thời khóa biểu';
            
            document.getElementById('timetableDay').value = day;
            
            startTime24h = `${hour.toString().padStart(2, '0')}:${minute.toString().padStart(2, '0')}`;
            
            let endHour = hour + 1;
            let endMinute = minute;
            if (endHour >= 24) {
                endHour = 23;
                endMinute = 59;
            }
            endTime24h = `${endHour.toString().padStart(2, '0')}:${endMinute.toString().padStart(2, '0')}`;
            
            // Reset form
            document.getElementById('timetableSubject').value = '';
            document.getElementById('subjectDescription').value = '';
            document.getElementById('subjectPriority').value = 'medium';
            document.getElementById('timetableColor').value = '#4a6fa5';
            document.getElementById('timetableNote').value = '';
            document.getElementById('noteContent').classList.remove('show');
            document.getElementById('notePreview').classList.remove('show');
            document.getElementById('noteToggle').textContent = '+ Thêm ghi chú';
            
            // Ẩn nút chỉnh sửa
            document.getElementById('editActions').style.display = 'none';
            document.getElementById('submitTimetableBtn').textContent = 'Thêm vào TKB';
            
            initializeTimeDropdowns();
            document.getElementById('timetableModal').style.display = 'flex';
        }

        function closeTimetableModal() {
            document.getElementById('timetableModal').style.display = 'none';
        }

        function addToTimetable(event) {
            event.preventDefault();
            
            const editMode = document.getElementById('editMode').value === 'true';
            const timetableId = document.getElementById('editTimetableId').value;
            const day = editMode ? parseInt(document.getElementById('editDay').value) : parseInt(document.getElementById('timetableDay').value);
            const weekKey = editMode ? document.getElementById('editWeekKey').value : getWeekKey(currentWeek);
            
            const subjectSelect = document.getElementById('timetableSubject');
            const subjectId = subjectSelect.value;
            const color = document.getElementById('timetableColor').value;
            const note = document.getElementById('timetableNote').value.trim();
            const description = document.getElementById('subjectDescription').value.trim();
            const priority = document.getElementById('subjectPriority').value;
            const autoCreateTask = document.getElementById('autoCreateTask').checked;
            
            if (!subjectId) {
                alert('Vui lòng chọn môn học');
                return;
            }
            
            const duration = calculateDuration(startTime24h, endTime24h);
            if (duration.totalMinutes <= 0) {
                alert('Thời gian kết thúc phải sau thời gian bắt đầu');
                return;
            }
            
            // Tìm môn học trong danh sách
            let subject = defaultSubjects.find(subj => subj.id === subjectId);
            let subjectName = '';
            let subjectDescription = description;
            
            if (!subject) {
                const tasks = loadTasksFromStorage();
                subject = tasks.find(task => task.id === subjectId);
            }
            
            if (subject) {
                subjectName = subject.name;
                subjectDescription = description || subject.description;
            } else {
                alert('Môn học không tồn tại');
                return;
            }
            
            const timetable = loadTimetableFromStorage();
            const dayKey = `${weekKey}-${day}`;
            
            if (!timetable[dayKey]) {
                timetable[dayKey] = {};
            }
            
            // Tạo ID cho mỗi môn học trong TKB 
            const newTimetableId = editMode ? timetableId : generateId();
            
            // Tạo thông tin môn học
            const subjectInfo = {
                id: subjectId,
                timetableId: newTimetableId,
                name: subjectName,
                description: subjectDescription,
                priority: priority,
                color: color,
                startTime: startTime24h,
                endTime: endTime24h,
                duration: duration.totalMinutes,
                note: note || null
            };
            
            // Sử dụng timetableId làm key để tránh ghi đè
            timetable[dayKey][newTimetableId] = subjectInfo;
            
            saveTimetableToStorage(timetable);
            
            // Cập nhật hiển thị
            if (isDetailedView) {
                generateDetailedTimetable();
            } else {
                generateTimetable();
            }
            
            closeTimetableModal();
            
            // Tự động tạo task trong Lịch học nếu được chọn
            if (autoCreateTask && !editMode) {
                const newTask = createTaskFromTimetable(subjectInfo, day, startTime24h, endTime24h);
                const tasks = loadTasksFromStorage();
                
                // Kiểm tra xem task đã tồn tại chưa
                const existingTaskIndex = tasks.findIndex(task => task.id === newTask.id);
                if (existingTaskIndex === -1) {
                    tasks.push(newTask);
                } else {
                    tasks[existingTaskIndex] = newTask;
                }
                
                saveTasksToStorage(tasks);
                
                showNotification("Thành công", `Đã ${editMode ? 'cập nhật' : 'thêm'} "${subjectName}" vào TKB và Lịch học`, "success");
            } else {
                showNotification("Thành công", `Đã ${editMode ? 'cập nhật' : 'thêm'} "${subjectName}" vào TKB`, "success");
            }
            
            renderTasks();
            updateNotificationBadge();
        }

        function createTaskFromTimetable(subjectInfo, day, startTime, endTime) {
            const now = new Date();
            const startOfWeek = new Date(now);
            startOfWeek.setDate(now.getDate() - now.getDay() + 1 + (currentWeek * 7));
            
            const studyDate = new Date(startOfWeek);
            studyDate.setDate(startOfWeek.getDate() + (day === 0 ? 6 : day - 1));
            
            const [hours, minutes] = startTime.split(':').map(Number);
            studyDate.setHours(hours, minutes, 0, 0);
            
            const dueDate = new Date(studyDate);
            dueDate.setDate(studyDate.getDate() + 7);
            
            const newTask = {
                id: subjectInfo.id,
                name: subjectInfo.name,
                description: subjectInfo.description || `Buổi học ${subjectInfo.name} từ ${startTime} đến ${endTime}`,
                dueDate: dueDate.toISOString().slice(0, 16),
                priority: subjectInfo.priority || 'medium',
                duration: subjectInfo.duration || 60,
                completed: false,
                createdAt: new Date().toISOString(),
                inTimetable: true,
                fromTimetable: true
            };
            
            return newTask;
        }

        function quickAddToTimetable(taskId) {
            const tasks = loadTasksFromStorage();
            const task = tasks.find(t => t.id === taskId);
            
            if (!task) return;
            
            document.getElementById('timetableSubject').value = taskId;
            document.getElementById('subjectDescription').value = task.description || '';
            document.getElementById('subjectPriority').value = task.priority;
            document.getElementById('timetableModal').style.display = 'flex';
            
            const now = new Date();
            const startHour = now.getHours();
            const startMinute = Math.ceil(now.getMinutes() / 5) * 5;
            
            startTime24h = `${startHour.toString().padStart(2, '0')}:${startMinute.toString().padStart(2, '0')}`;
            
            const endTime = new Date(now.getTime() + 60 * 60 * 1000);
            const endHour = endTime.getHours();
            const endMinute = endTime.getMinutes();
            
            endTime24h = `${endHour.toString().padStart(2, '0')}:${endMinute.toString().padStart(2, '0')}`;
            
            initializeTimeDropdowns();
        }

        function removeFromTimetable(day, timetableId, weekKey) {
            if (confirm('Bạn có chắc chắn muốn xóa môn học này khỏi thời khóa biểu?')) {
                const timetable = loadTimetableFromStorage();
                const dayKey = `${weekKey}-${day}`;
                
                if (timetable[dayKey] && timetable[dayKey][timetableId]) {
                    const subjectName = timetable[dayKey][timetableId].name;
                    delete timetable[dayKey][timetableId];
                    
                    // Nếu ngày đó không còn môn học nào, xóa luôn key của ngày
                    if (Object.keys(timetable[dayKey]).length === 0) {
                        delete timetable[dayKey];
                    }
                    
                    saveTimetableToStorage(timetable);
                    
                    // Cập nhật hiển thị
                    if (isDetailedView) {
                        generateDetailedTimetable();
                    } else {
                        generateTimetable();
                    }
                    
                    showNotification("Đã xóa", `Đã xóa "${subjectName}" khỏi TKB`, "info");
                    
                    // Render lại danh sách task
                    renderTasks();
                    updateNotificationBadge();
                }
            }
        }

        function clearTimetable() {
            if (confirm('Bạn có chắc chắn muốn xóa toàn bộ thời khóa biểu?')) {
                saveTimetableToStorage({});
                
                if (isDetailedView) {
                    generateDetailedTimetable();
                } else {
                    generateTimetable();
                }
                
                showNotification("Đã xóa", "Đã xóa toàn bộ thời khóa biểu", "info");
                
                renderTasks();
                updateNotificationBadge();
            }
        }

        // Xử lý sự kiện cho nút xóa trong chế độ chỉnh sửa
        function setupEditActions() {
            document.getElementById('deleteSubjectBtn').addEventListener('click', function() {
                const timetableId = document.getElementById('editTimetableId').value;
                const day = parseInt(document.getElementById('editDay').value);
                const weekKey = document.getElementById('editWeekKey').value;
                
                if (confirm('Bạn có chắc chắn muốn xóa môn học này?')) {
                    removeFromTimetable(day, timetableId, weekKey);
                    closeTimetableModal();
                }
            });
            
            document.getElementById('cancelEditBtn').addEventListener('click', function() {
                closeTimetableModal();
            });
        }

        // Sửa hàm populateTimetableSubjects để chỉ hiển thị 3 môn học cố định
        function populateTimetableSubjects() {
            const subjectSelect = document.getElementById('timetableSubject');
            
            // Xóa tất cả các option hiện có
            subjectSelect.innerHTML = '<option value="">Chọn môn học</option>';
            
            // hiển thị 3 môn
            defaultSubjects.forEach(subject => {
                const option = document.createElement('option');
                option.value = subject.id;
                option.textContent = subject.name;
                subjectSelect.appendChild(option);
            });
            
        }

        function initializeTimeDropdowns() {
            const startHour = document.getElementById('startHour');
            const startMinute = document.getElementById('startMinute');
            const endHour = document.getElementById('endHour');
            const endMinute = document.getElementById('endMinute');

            startHour.innerHTML = '';
            startMinute.innerHTML = '';
            endHour.innerHTML = '';
            endMinute.innerHTML = '';

            for (let i = 0; i <= 23; i++) {
                const option = document.createElement('option');
                option.value = i;
                option.textContent = i.toString().padStart(2, '0');
                startHour.appendChild(option.cloneNode(true));
                endHour.appendChild(option);
            }

            for (let i = 0; i < 60; i += 5) {
                const option = document.createElement('option');
                option.value = i;
                option.textContent = i.toString().padStart(2, '0');
                startMinute.appendChild(option.cloneNode(true));
                endMinute.appendChild(option);
            }

            const [startHours, startMinutes] = startTime24h.split(':').map(Number);
            const [endHours, endMinutes] = endTime24h.split(':').map(Number);

            startHour.value = startHours;
            startMinute.value = startMinutes;
            endHour.value = endHours;
            endMinute.value = endMinutes;

            updateTimeDisplay();
        }

        function updateTimeDisplay() {
            const startHour = document.getElementById('startHour').value;
            const startMinute = document.getElementById('startMinute').value;
            const endHour = document.getElementById('endHour').value;
            const endMinute = document.getElementById('endMinute').value;

            startTime24h = `${parseInt(startHour).toString().padStart(2, '0')}:${startMinute.padStart(2, '0')}`;
            endTime24h = `${parseInt(endHour).toString().padStart(2, '0')}:${endMinute.padStart(2, '0')}`;

            document.getElementById('timeDisplay').textContent = 
                `Thời gian: ${startTime24h} - ${endTime24h}`;

            updateDurationDisplay();
        }

        function updateDurationDisplay() {
            const duration = calculateDuration(startTime24h, endTime24h);
            
            let durationText = '';
            if (duration.hours > 0) {
                durationText = `Thời lượng: ${duration.hours} giờ ${duration.minutes} phút`;
            } else {
                durationText = `Thời lượng: ${duration.minutes} phút`;
            }
            
            document.getElementById('durationDisplay').textContent = durationText;
        }

        function setupTimeEventListeners() {
            document.getElementById('startHour').addEventListener('change', updateTimeDisplay);
            document.getElementById('startMinute').addEventListener('change', updateTimeDisplay);
            document.getElementById('endHour').addEventListener('change', updateTimeDisplay);
            document.getElementById('endMinute').addEventListener('change', updateTimeDisplay);
        }

        function setupNoteSection() {
            const noteToggle = document.getElementById('noteToggle');
            const noteContent = document.getElementById('noteContent');
            const noteTextarea = document.getElementById('timetableNote');
            const notePreview = document.getElementById('notePreview');
            const notePreviewText = document.getElementById('notePreviewText');

            noteToggle.addEventListener('click', function() {
                const isShowing = noteContent.classList.contains('show');
                if (isShowing) {
                    noteContent.classList.remove('show');
                    notePreview.classList.remove('show');
                    this.textContent = '+ Thêm ghi chú';
                } else {
                    noteContent.classList.add('show');
                    this.textContent = '- Ẩn ghi chú';
                    updateNotePreview();
                }
            });

            noteTextarea.addEventListener('input', updateNotePreview);

            function updateNotePreview() {
                const noteText = noteTextarea.value.trim();
                if (noteText) {
                    notePreviewText.textContent = noteText;
                    notePreview.classList.add('show');
                } else {
                    notePreview.classList.remove('show');
                }
            }
        }

        function setupTabs() {
            const tabs = document.querySelectorAll('.tab');
            
            tabs.forEach(tab => {
                tab.addEventListener('click', () => {
                    document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
                    document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
                    
                    tab.classList.add('active');
                    
                    const tabId = tab.getAttribute('data-tab');
                    document.getElementById(`${tabId}-tab`).classList.add('active');
                    
                    if (tabId === 'tasks') {
                        setTimeout(renderTasks, 100);
                    } else if (tabId === 'timetable') {
                        setTimeout(() => {
                            if (isDetailedView) {
                                generateDetailedTimetable();
                            } else {
                                generateTimetable();
                            }
                        }, 100);
                    }
                });
            });
        }

        function setupColorPreview() {
            const colorSelect = document.getElementById('timetableColor');
            const colorPreview = document.getElementById('colorPreview');
            
            colorSelect.addEventListener('change', () => {
                colorPreview.style.backgroundColor = colorSelect.value;
            });
        }

        function switchToTab(tabName) {
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
            
            document.querySelector(`[data-tab="${tabName}"]`).classList.add('active');
            document.getElementById(`${tabName}-tab`).classList.add('active');
            
            if (tabName === 'tasks') {
                setTimeout(renderTasks, 100);
            } else if (tabName === 'timetable') {
                setTimeout(() => {
                    if (isDetailedView) {
                        generateDetailedTimetable();
                    } else {
                        generateTimetable();
                    }
                }, 100);
            }
        }

        // Tạo ứng dụng
        function initApp() {
            appSettings = loadAppSettings();
            applySettings();
            
            updateCurrentDate();
            renderTasks();
            updateStats();
            updateNotificationBadge();
            
            generateTimetable();
            updateWeekDisplay();
            populateTimetableSubjects();
            initializeTimeDropdowns();
            setupTimeEventListeners();
            setupNoteSection();
            setupStatsTabs(); 
            
            // Thông báo hk
            initStudyNotifications();
            
            // yêu cầu cấp quyền thông báo
            setTimeout(() => {
                requestNotificationPermission();
            }, 1000);
            
            document.getElementById('taskForm').addEventListener('submit', addTask);
            document.getElementById('timetableForm').addEventListener('submit', addToTimetable);
            document.getElementById('addToTimetable').addEventListener('click', () => openTimetableModal(1, 7));
            document.getElementById('clearTimetable').addEventListener('click', clearTimetable);
            
            document.querySelector('#timetableModal .close-modal').addEventListener('click', closeTimetableModal);
            
            document.getElementById('timetableModal').addEventListener('click', function(e) {
                if (e.target === this) {
                    closeTimetableModal();
                }
            });
            
            document.getElementById('prevWeek').addEventListener('click', () => {
                currentWeek--;
                updateWeekDisplay();
                if (isDetailedView) {
                    generateDetailedTimetable();
                } else {
                    generateTimetable();
                }
            });
            
            document.getElementById('nextWeek').addEventListener('click', () => {
                currentWeek++;
                updateWeekDisplay();
                if (isDetailedView) {
                    generateDetailedTimetable();
                } else {
                    generateTimetable();
                }
            });
            
            setupTabs();
            setupColorPreview();
            
            setInterval(updateCurrentDate, 60000);
            setInterval(updateNotificationBadge, 60000);
            
            // Show welcome notification với nút xem lịch học hôm nay
            setTimeout(() => {
                const notificationId = showNotification(
                    "Chào mừng!",
                    "Hệ thống quản lý thời gian học tập đã sẵn sàng.\nBắt đầu lập kế hoạch học tập ngay!",
                    "info",
                    8000
                );

                // Thêm nút xem lịch học hôm nay
                const notification = document.getElementById(`notification-${notificationId}`);
                if (notification) {
                    const actionsContainer = document.createElement('div');
                    actionsContainer.className = 'study-actions';
                    
                    actionsContainer.innerHTML = `
                        <button class="study-action-btn start" onclick="showTodaysSchedule(); closeNotification('${notificationId}')" style="margin: 5px 0;">
                            📅 Xem lịch học hôm nay
                        </button>
                    `;
                    
                    notification.querySelector('.notification-content').appendChild(actionsContainer);
                }
            }, 2000);
        }

        // Đồng bộ thông báo
        document.addEventListener('visibilitychange', function() {
            if (document.hidden) {
                console.log('Tab không active, thông báo sẽ hiển thị trên desktop');
            }
        });

        // Chạy ứng dụng khi trang đã tải xong
        document.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>
