<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quản lý Thời gian Học tập</title>
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
        }

        .tab-switch-btn:hover {
            background: rgba(255, 255, 255, 0.3);
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

        /* Styles for timetable */
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

        /* Modal styles */
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
            max-width: 500px;
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

        /* CSS cho phần chọn thời gian 24h */
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

        /* CSS cho phần ghi chú */
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
            margin-top: 10px;
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

        /* CSS cho timetable indicator */
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

        /* Notification styles */
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

        /* Settings panel */
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

        /* Responsive styles */
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
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <div class="header-content">
                <h1>📚 Quản lý Thời gian Học tập</h1>
                <div class="header-navigation">
                    <button onclick="switchToTab('tasks')" class="tab-switch-btn">📚 Môn học</button>
                    <button onclick="switchToTab('timetable')" class="tab-switch-btn">📅 Thời khóa biểu</button>
                    <button onclick="showWeeklySchedule()" class="tab-switch-btn">📋 Lịch tuần</button>
                    <button onclick="openSettings()" class="tab-switch-btn">⚙️ Cài đặt</button>
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
                        <h2>Thêm môn học mới</h2>
                        <form id="taskForm">
                            <div class="form-group">
                                <label for="taskName">Tên môn học</label>
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
                            <button type="submit" class="btn-success">Thêm môn học</button>
                        </form>
                    </div>

                    <div class="card">
                        <h2>Lịch học của tôi</h2>
                        <div id="taskList">
                            <div class="empty-state">
                                <i>📚</i>
                                <p>Chưa có môn học nào. Hãy thêm môn học đầu tiên!</p>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="right-column">
                    <div class="card">
                        <h2>Thống kê học tập</h2>
                        <div class="stats">
                            <div class="stat-card">
                                <div class="stat-value" id="totalTasks">0</div>
                                <div class="stat-label">Tổng môn học</div>
                            </div>
                            <div class="stat-card">
                                <div class="stat-value" id="completedTasks">0</div>
                                <div class="stat-label">Đã hoàn thành</div>
                            </div>
                            <div class="stat-card">
                                <div class="stat-value" id="pendingTasks">0</div>
                                <div class="stat-label">Chưa hoàn thành</div>
                            </div>
                            <div class="stat-card">
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
                        <h2>Môn học sắp đến hạn</h2>
                        <div id="upcomingTasks">
                            <div class="empty-state">
                                <i>⏰</i>
                                <p>Không có môn học nào sắp đến hạn</p>
                            </div>
                        </div>
                    </div>

                    <div class="card">
                        <h2>Lời khuyên học tập</h2>
                        <ul id="studyTips">
                            <li>Chia nhỏ thời gian học thành các phiên 25-30 phút</li>
                            <li>Nghỉ ngơi 5 phút sau mỗi phiên học</li>
                            <li>Ôn tập lại kiến thức sau 24 giờ</li>
                            <li>Đặt mục tiêu rõ ràng cho mỗi buổi học</li>
                            <li>Tạo môi trường học tập không bị phân tâm</li>
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
                    </div>
                </div>
                <div class="timetable-container">
                    <table class="timetable">
                        <thead>
                            <tr>
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
                            <!-- Timetable will be generated here -->
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>

    <!-- Notification Container -->
    <div class="notification-container" id="notificationContainer"></div>

    <!-- Settings Panel -->
    <div class="settings-overlay" id="settingsOverlay"></div>
    <div class="settings-panel" id="settingsPanel">
        <div class="settings-header">
            <h2>Cài đặt Thông báo</h2>
            <button class="close-modal" onclick="closeSettings()">&times;</button>
        </div>
        
        <div class="form-group">
            <label>
                <input type="checkbox" id="enableNotifications" checked>
                Bật thông báo
            </label>
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
            <label>
                <input type="checkbox" id="desktopNotifications" checked>
                Hiển thị thông báo trên desktop
            </label>
        </div>
        
        <div class="form-group">
            <label>
                <input type="checkbox" id="browserNotifications">
                Cho phép thông báo trình duyệt
            </label>
        </div>
        
        <div class="form-group">
            <button class="btn-success" onclick="testNotification()">Kiểm tra thông báo</button>
            <button class="btn-danger" onclick="clearAllNotifications()">Xóa tất cả thông báo</button>
        </div>
        
        <div class="form-group">
            <h3>Lịch sử thông báo</h3>
            <div id="notificationHistory" style="max-height: 200px; overflow-y: auto; background: #f8f9fa; padding: 10px; border-radius: 4px;">
                <!-- Notification history will be displayed here -->
            </div>
        </div>
    </div>

    <!-- Modal for adding subject to timetable -->
    <div class="modal" id="timetableModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Thêm môn học vào thời khóa biểu</h2>
                <button class="close-modal">&times;</button>
            </div>
            <form id="timetableForm" class="timetable-form">
                <div class="form-group">
                    <label for="timetableSubject">Môn học</label>
                    <select id="timetableSubject" required>
                        <option value="">Chọn môn học</option>
                        <!-- Default subjects will be added here -->
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
                                    <!-- Giờ sẽ được thêm bằng JavaScript -->
                                </select>
                                <div class="time-label">Giờ</div>
                            </div>
                            <div class="time-column">
                                <select class="time-dropdown" id="startMinute">
                                    <!-- Phút sẽ được thêm bằng JavaScript -->
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
                                    <!-- Giờ sẽ được thêm bằng JavaScript -->
                                </select>
                                <div class="time-label">Giờ</div>
                            </div>
                            <div class="time-column">
                                <select class="time-dropdown" id="endMinute">
                                    <!-- Phút sẽ được thêm bằng JavaScript -->
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

                <!-- Phần ghi chú mới -->
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
                        <option value="#4a6fa5">Xanh dương</option>
                        <option value="#ff7e5f">Cam</option>
                        <option value="#28a745">Xanh lá</option>
                        <option value="#6f42c1">Tím</option>
                        <option value="#e83e8c">Hồng</option>
                        <option value="#fd7e14">Cam đậm</option>
                        <option value="#20c997">Xanh ngọc</option>
                        <option value="#6610f2">Tím đậm</option>
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
                
                <button type="submit" class="btn-success">Thêm vào TKB</button>
            </form>
        </div>
    </div>

    <footer>
        <div class="container">
            <p>Ứng dụng Quản lý Thời gian Học tập &copy; 2023 - Hoạt động trên mọi thiết bị</p>
        </div>
    </footer>

    <script>
        // Default subjects
        const defaultSubjects = [
            { id: 'math', name: 'Toán', description: 'Môn Toán học' },
            { id: 'physics', name: 'Lý', description: 'Môn Vật lý' },
            { id: 'english', name: 'Anh', description: 'Môn Tiếng Anh' }
        ];

        // Biến để lưu thời gian
        let startTime24h = "07:00";
        let endTime24h = "08:00";

        // Notification system
        let notificationCheckInterval;
        let notificationSettings = {
            enabled: true,
            timeBefore: 15, // minutes
            sound: 'default',
            desktop: true,
            browser: false
        };

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

        function saveNotificationSettings(settings) {
            localStorage.setItem('notificationSettings', JSON.stringify(settings));
        }

        function loadNotificationSettings() {
            const settings = localStorage.getItem('notificationSettings');
            return settings ? JSON.parse(settings) : notificationSettings;
        }

        function saveNotificationHistory(history) {
            localStorage.setItem('notificationHistory', JSON.stringify(history));
        }

        function loadNotificationHistory() {
            const history = localStorage.getItem('notificationHistory');
            return history ? JSON.parse(history) : [];
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

        // NOTIFICATION SYSTEM
        function showNotification(title, message, type = 'info', duration = 5000) {
            if (!notificationSettings.enabled) return;

            const notificationContainer = document.getElementById('notificationContainer');
            const notificationId = generateId();
            
            const notification = document.createElement('div');
            notification.className = `notification ${type}`;
            notification.id = `notification-${notificationId}`;
            
            const icons = {
                info: 'ℹ️',
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
            
            // Hiệu ứng hiện lên
            setTimeout(() => {
                notification.classList.add('show');
            }, 100);
            
            // Lưu vào lịch sử
            const history = loadNotificationHistory();
            history.unshift({
                id: notificationId,
                title,
                message,
                type,
                timestamp: new Date().toISOString()
            });
            
            // Giới hạn lịch sử 50 mục
            if (history.length > 50) {
                history.pop();
            }
            
            saveNotificationHistory(history);
            updateNotificationHistory();
            
            // Tự động đóng sau duration
            if (duration > 0) {
                setTimeout(() => {
                    closeNotification(notificationId);
                }, duration);
            }
            
            // Phát âm thanh nếu được bật
            playNotificationSound();
            
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

        function playNotificationSound() {
            if (notificationSettings.sound === 'none') return;
            
            // Tạo âm thanh đơn giản
            try {
                const audioContext = new (window.AudioContext || window.webkitAudioContext)();
                const oscillator = audioContext.createOscillator();
                const gainNode = audioContext.createGain();
                
                oscillator.connect(gainNode);
                gainNode.connect(audioContext.destination);
                
                if (notificationSettings.sound === 'bell') {
                    oscillator.frequency.setValueAtTime(800, audioContext.currentTime);
                    oscillator.frequency.setValueAtTime(600, audioContext.currentTime + 0.1);
                } else if (notificationSettings.sound === 'chime') {
                    oscillator.frequency.setValueAtTime(523.25, audioContext.currentTime); // C5
                    oscillator.frequency.setValueAtTime(659.25, audioContext.currentTime + 0.1); // E5
                } else {
                    oscillator.frequency.setValueAtTime(600, audioContext.currentTime);
                }
                
                gainNode.gain.setValueAtTime(0.3, audioContext.currentTime);
                gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.5);
                
                oscillator.start(audioContext.currentTime);
                oscillator.stop(audioContext.currentTime + 0.5);
            } catch (error) {
                console.log('Không thể phát âm thanh thông báo');
            }
        }

        // Hàm kiểm tra và thông báo lịch học sắp diễn ra
        function checkUpcomingClasses() {
            if (!notificationSettings.enabled) return;
            
            const timetable = loadTimetableFromStorage();
            const now = new Date();
            const currentDay = now.getDay(); // 0: Chủ nhật, 1: Thứ 2, ..., 6: Thứ 7
            const currentTime = now.getHours() * 60 + now.getMinutes(); // Thời gian hiện tại tính bằng phút
            
            // Duyệt qua tất cả các ngày trong tuần hiện tại
            Object.keys(timetable).forEach(dayKey => {
                const daySchedule = timetable[dayKey];
                const dayIndex = parseInt(dayKey.split('-')[1]);
                
                // Chỉ kiểm tra ngày hiện tại
                if (dayIndex === currentDay) {
                    // Duyệt qua tất cả môn học trong ngày
                    Object.values(daySchedule).forEach(subject => {
                        const [startHour, startMinute] = subject.startTime.split(':').map(Number);
                        const classStartTime = startHour * 60 + startMinute; // Thời gian bắt đầu tính bằng phút
                        const timeDiff = classStartTime - currentTime;
                        
                        // Kiểm tra nếu sắp đến giờ học (trong khoảng thời gian cài đặt)
                        if (timeDiff > 0 && timeDiff <= notificationSettings.timeBefore) {
                            // Kiểm tra xem đã thông báo chưa
                            const notificationKey = `class_${subject.id}_${dayKey}_${subject.startTime}`;
                            if (!localStorage.getItem(notificationKey)) {
                                const timeText = timeDiff < 60 ? 
                                    `${timeDiff} phút` : 
                                    `${Math.floor(timeDiff / 60)} giờ ${timeDiff % 60} phút`;
                                
                                showNotification(
                                    `⏰ Sắp đến giờ học`,
                                    `Môn "${subject.name}" sẽ bắt đầu lúc ${subject.startTime} (sau ${timeText})`,
                                    'warning',
                                    10000
                                );
                                
                                // Đánh dấu đã thông báo để tránh thông báo lặp lại
                                localStorage.setItem(notificationKey, 'true');
                                
                                // Tự động xóa đánh dấu sau khi giờ học qua
                                setTimeout(() => {
                                    localStorage.removeItem(notificationKey);
                                }, (timeDiff + 60) * 60 * 1000); // +60 phút sau giờ học
                            }
                        }
                        
                        // Thông báo khi đến đúng giờ học
                        if (timeDiff === 0 && !localStorage.getItem(`class_started_${subject.id}_${dayKey}`)) {
                            showNotification(
                                `🎯 Đến giờ học`,
                                `Môn "${subject.name}" bắt đầu ngay bây giờ!`,
                                'info',
                                15000
                            );
                            
                            localStorage.setItem(`class_started_${subject.id}_${dayKey}`, 'true');
                            
                            // Tự động xóa đánh dấu sau 2 giờ
                            setTimeout(() => {
                                localStorage.removeItem(`class_started_${subject.id}_${dayKey}`);
                            }, 2 * 60 * 60 * 1000);
                        }
                    });
                }
            });
        }

        function checkUpcomingTasks() {
            if (!notificationSettings.enabled) return;
            
            const tasks = loadTasksFromStorage();
            const now = new Date();
            
            tasks.forEach(task => {
                if (task.completed) return;
                
                const dueDate = new Date(task.dueDate);
                const timeDiff = dueDate - now;
                const minutesDiff = Math.floor(timeDiff / (1000 * 60));
                
                // Kiểm tra nếu sắp đến hạn (trong khoảng thời gian cài đặt)
                if (minutesDiff > 0 && minutesDiff <= notificationSettings.timeBefore) {
                    // Kiểm tra xem đã thông báo chưa
                    if (!task.notified) {
                        const timeText = minutesDiff < 60 ? 
                            `${minutesDiff} phút` : 
                            `${Math.floor(minutesDiff / 60)} giờ ${minutesDiff % 60} phút`;
                        
                        showNotification(
                            `📚 Sắp đến hạn`,
                            `Môn "${task.name}" sẽ đến hạn sau ${timeText}`,
                            'warning',
                            10000
                        );
                        
                        // Đánh dấu đã thông báo
                        task.notified = true;
                        saveTasksToStorage(tasks);
                    }
                }
                
                // Kiểm tra nếu đã quá hạn
                if (timeDiff < 0 && !task.overdueNotified) {
                    showNotification(
                        `❌ Đã quá hạn`,
                        `Môn "${task.name}" đã quá hạn`,
                        'error',
                        15000
                    );
                    
                    task.overdueNotified = true;
                    saveTasksToStorage(tasks);
                }
            });
        }

        function startNotificationChecker() {
            // Kiểm tra mỗi phút
            notificationCheckInterval = setInterval(() => {
                checkUpcomingTasks();
                checkUpcomingClasses();
            }, 60000);
            
            // Kiểm tra ngay lập tức
            checkUpcomingTasks();
            checkUpcomingClasses();
        }

        function stopNotificationChecker() {
            if (notificationCheckInterval) {
                clearInterval(notificationCheckInterval);
            }
        }

        // SETTINGS PANEL
        function openSettings() {
            document.getElementById('settingsPanel').classList.add('open');
            document.getElementById('settingsOverlay').classList.add('show');
            loadSettingsToForm();
        }

        function closeSettings() {
            document.getElementById('settingsPanel').classList.remove('open');
            document.getElementById('settingsOverlay').classList.remove('show');
            saveSettingsFromForm();
        }

        function loadSettingsToForm() {
            const settings = loadNotificationSettings();
            document.getElementById('enableNotifications').checked = settings.enabled;
            document.getElementById('notificationTime').value = settings.timeBefore;
            document.getElementById('notificationSound').value = settings.sound;
            document.getElementById('desktopNotifications').checked = settings.desktop;
            document.getElementById('browserNotifications').checked = settings.browser;
            
            updateNotificationHistory();
        }

        function saveSettingsFromForm() {
            notificationSettings.enabled = document.getElementById('enableNotifications').checked;
            notificationSettings.timeBefore = parseInt(document.getElementById('notificationTime').value);
            notificationSettings.sound = document.getElementById('notificationSound').value;
            notificationSettings.desktop = document.getElementById('desktopNotifications').checked;
            notificationSettings.browser = document.getElementById('browserNotifications').checked;
            
            saveNotificationSettings(notificationSettings);
            
            // Khởi động lại hệ thống thông báo
            stopNotificationChecker();
            if (notificationSettings.enabled) {
                startNotificationChecker();
            }
        }

        function updateNotificationHistory() {
            const history = loadNotificationHistory();
            const historyContainer = document.getElementById('notificationHistory');
            
            if (history.length === 0) {
                historyContainer.innerHTML = '<p style="color: #666; text-align: center;">Chưa có thông báo nào</p>';
                return;
            }
            
            historyContainer.innerHTML = history.slice(0, 10).map(notif => `
                <div style="padding: 8px; margin-bottom: 5px; background: white; border-radius: 4px; border-left: 3px solid ${getNotificationColor(notif.type)}">
                    <div style="font-weight: 600; font-size: 0.9rem;">${notif.title}</div>
                    <div style="font-size: 0.8rem; color: #666;">${notif.message}</div>
                    <div style="font-size: 0.7rem; color: #999;">${new Date(notif.timestamp).toLocaleString('vi-VN')}</div>
                </div>
            `).join('');
        }

        function getNotificationColor(type) {
            const colors = {
                info: '#4a6fa5',
                warning: '#ffc107',
                error: '#dc3545',
                success: '#28a745'
            };
            return colors[type] || '#4a6fa5';
        }

        function testNotification() {
            showNotification(
                "Kiểm tra thông báo",
                "Đây là thông báo kiểm tra từ hệ thống",
                "info",
                5000
            );
        }

        function clearAllNotifications() {
            const notificationContainer = document.getElementById('notificationContainer');
            notificationContainer.innerHTML = '';
            saveNotificationHistory([]);
            updateNotificationHistory();
        }

        // Đồng bộ hóa tự động giữa Lịch học và Thời khóa biểu
        function autoSyncTimetableStatus() {
            const tasks = loadTasksFromStorage();
            const timetable = loadTimetableFromStorage();
            
            // Tạo map để theo dõi môn học nào đã có trong TKB
            const subjectsInTimetable = {};
            
            // Duyệt qua tất cả các ngày trong TKB
            Object.values(timetable).forEach(daySchedule => {
                Object.values(daySchedule).forEach(subject => {
                    subjectsInTimetable[subject.id] = true;
                });
            });
            
            // Cập nhật trạng thái cho từng task
            const updatedTasks = tasks.map(task => {
                return {
                    ...task,
                    inTimetable: !!subjectsInTimetable[task.id]
                };
            });
            
            saveTasksToStorage(updatedTasks);
            return updatedTasks;
        }

        // Tạo task mới từ thông tin TKB
        function createTaskFromTimetable(subjectInfo, day, startTime, endTime) {
            const now = new Date();
            const startOfWeek = new Date(now);
            startOfWeek.setDate(now.getDate() - now.getDay() + 1 + (currentWeek * 7)); // Thứ 2 là đầu tuần
            
            // Tính ngày học dựa trên thứ và tuần hiện tại
            const studyDate = new Date(startOfWeek);
            studyDate.setDate(startOfWeek.getDate() + (day === 0 ? 6 : day - 1)); // Điều chỉnh cho Chủ nhật
            
            // Đặt thời gian cho ngày học
            const [hours, minutes] = startTime.split(':').map(Number);
            studyDate.setHours(hours, minutes, 0, 0);
            
            // Thời hạn là ngày học + 1 tuần (7 ngày)
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
                fromTimetable: true // Đánh dấu task được tạo từ TKB
            };
            
            return newTask;
        }

        // Thêm task mới
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
            
            // Hiển thị thông báo
            showNotification("Thành công", `Đã thêm môn học "${name}"`, "success");
            
            // Reset form
            document.getElementById('taskForm').reset();
        }

        // Xóa task
        function deleteTask(taskId) {
            if (confirm('Bạn có chắc chắn muốn xóa môn học này?')) {
                const tasks = loadTasksFromStorage();
                const taskToDelete = tasks.find(task => task.id === taskId);
                const updatedTasks = tasks.filter(task => task.id !== taskId);
                saveTasksToStorage(updatedTasks);
                
                // Xóa khỏi TKB nếu có
                const timetable = loadTimetableFromStorage();
                let timetableUpdated = false;
                
                Object.keys(timetable).forEach(dayKey => {
                    Object.keys(timetable[dayKey]).forEach(timeSlot => {
                        if (timetable[dayKey][timeSlot].id === taskId) {
                            delete timetable[dayKey][timeSlot];
                            timetableUpdated = true;
                        }
                    });
                });
                
                if (timetableUpdated) {
                    saveTimetableToStorage(timetable);
                    generateTimetable();
                }
                
                renderTasks();
                updateStats();
                
                // Hiển thị thông báo
                showNotification("Đã xóa", `Đã xóa môn học "${taskToDelete.name}"`, "info");
            }
        }

        // Đánh dấu task là đã hoàn thành
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
        }

        // Hiển thị danh sách task
        function renderTasks() {
            const taskList = document.getElementById('taskList');
            
            // Đồng bộ hóa trước khi render
            const tasks = autoSyncTimetableStatus();
            
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
                
                // Thêm indicator cho môn học đã có trong TKB
                const timetableIndicator = task.inTimetable ? 
                    '<span class="timetable-indicator" title="Đã có trong thời khóa biểu">📅</span>' : '';
                
                // Nút TKB - disabled nếu đã có trong TKB
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

        // Hiển thị các task sắp đến hạn
        function renderUpcomingTasks() {
            const upcomingTasksContainer = document.getElementById('upcomingTasks');
            const tasks = loadTasksFromStorage();
            const now = new Date();
            const next24Hours = new Date(now.getTime() + 24 * 60 * 60 * 1000);
            
            const upcomingTasks = tasks
                .filter(task => !task.completed && new Date(task.dueDate) > now && new Date(task.dueDate) <= next24Hours)
                .sort((a, b) => new Date(a.dueDate) - new Date(b.dueDate))
                .slice(0, 5); // Chỉ hiển thị 5 task gần nhất
            
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

        // Cập nhật thống kê
        function updateStats() {
            const tasks = loadTasksFromStorage();
            const totalTasks = tasks.length;
            const completedTasks = tasks.filter(task => task.completed).length;
            const pendingTasks = totalTasks - completedTasks;
            
            // Tính tổng thời gian học
            const totalStudyTime = tasks.reduce((total, task) => {
                return total + (task.completed ? task.duration : 0);
            }, 0);
            
            const studyHours = Math.floor(totalStudyTime / 60);
            const studyMinutes = totalStudyTime % 60;
            const studyTimeText = studyHours > 0 ? `${studyHours}h ${studyMinutes}p` : `${studyMinutes}p`;
            
            // Tính phần trăm hoàn thành
            const completionPercentage = totalTasks > 0 ? Math.round((completedTasks / totalTasks) * 100) : 0;
            
            document.getElementById('totalTasks').textContent = totalTasks;
            document.getElementById('completedTasks').textContent = completedTasks;
            document.getElementById('pendingTasks').textContent = pendingTasks;
            document.getElementById('studyTime').textContent = studyTimeText;
            document.getElementById('progressBar').style.width = `${completionPercentage}%`;
            document.getElementById('progressText').textContent = `${completionPercentage}% hoàn thành`;
        }

        // TIMETABLE FUNCTIONS
        let currentWeek = 0; // 0 means current week

        // Tính thời lượng từ startTime và endTime
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

        // Khởi tạo dropdown giờ và phút (24h)
        function initializeTimeDropdowns() {
            const startHour = document.getElementById('startHour');
            const startMinute = document.getElementById('startMinute');
            const endHour = document.getElementById('endHour');
            const endMinute = document.getElementById('endMinute');

            // Xóa options cũ
            startHour.innerHTML = '';
            startMinute.innerHTML = '';
            endHour.innerHTML = '';
            endMinute.innerHTML = '';

            // Thêm options cho giờ (0-23)
            for (let i = 0; i <= 23; i++) {
                const option = document.createElement('option');
                option.value = i;
                option.textContent = i.toString().padStart(2, '0');
                startHour.appendChild(option.cloneNode(true));
                endHour.appendChild(option);
            }

            // Thêm options cho phút (0-55, bước 5 phút)
            for (let i = 0; i < 60; i += 5) {
                const option = document.createElement('option');
                option.value = i;
                option.textContent = i.toString().padStart(2, '0');
                startMinute.appendChild(option.cloneNode(true));
                endMinute.appendChild(option);
            }

            // Thiết lập giá trị mặc định từ thời gian 24h
            const [startHours, startMinutes] = startTime24h.split(':').map(Number);
            const [endHours, endMinutes] = endTime24h.split(':').map(Number);

            startHour.value = startHours;
            startMinute.value = startMinutes;
            endHour.value = endHours;
            endMinute.value = endMinutes;

            updateTimeDisplay();
        }

        // Cập nhật hiển thị thời gian
        function updateTimeDisplay() {
            const startHour = document.getElementById('startHour').value;
            const startMinute = document.getElementById('startMinute').value;
            const endHour = document.getElementById('endHour').value;
            const endMinute = document.getElementById('endMinute').value;

            // Cập nhật thời gian 24h
            startTime24h = `${parseInt(startHour).toString().padStart(2, '0')}:${startMinute.padStart(2, '0')}`;
            endTime24h = `${parseInt(endHour).toString().padStart(2, '0')}:${endMinute.padStart(2, '0')}`;

            // Hiển thị thời gian
            document.getElementById('timeDisplay').textContent = 
                `Thời gian: ${startTime24h} - ${endTime24h}`;

            // Cập nhật thời lượng
            updateDurationDisplay();
        }

        // Cập nhật tính toán thời lượng
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

        // Quản lý phần ghi chú
        function setupNoteSection() {
            const noteToggle = document.getElementById('noteToggle');
            const noteContent = document.getElementById('noteContent');
            const noteTextarea = document.getElementById('timetableNote');
            const notePreview = document.getElementById('notePreview');
            const notePreviewText = document.getElementById('notePreviewText');

            // Toggle hiển thị phần ghi chú
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

            // Cập nhật preview khi người dùng nhập
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

        // Tạo thời khóa biểu với khung 24h - ĐÃ SỬA LỖI HOÀN TOÀN
        function generateTimetable() {
            const timetableBody = document.getElementById('timetableBody');
            timetableBody.innerHTML = '';
            
            // Tạo các hàng cho mỗi giờ từ 0:00 đến 23:00
            for (let hour = 0; hour < 24; hour++) {
                const row = document.createElement('tr');
                
                // Ô hiển thị giờ
                const timeCell = document.createElement('td');
                timeCell.className = 'time-slot';
                timeCell.innerHTML = `<strong>${hour.toString().padStart(2, '0')}:00</strong>`;
                row.appendChild(timeCell);
                
                // Tạo ô cho mỗi ngày trong tuần
                for (let day = 1; day <= 7; day++) {
                    const dayIndex = day === 7 ? 0 : day; // Chủ nhật là 0
                    const cell = document.createElement('td');
                    cell.dataset.day = dayIndex;
                    cell.dataset.hour = hour;
                    
                    // Thêm sự kiện click để thêm môn học
                    cell.addEventListener('click', () => openTimetableModal(dayIndex, hour));
                    
                    // Hiển thị môn học nếu có - ĐÃ SỬA LỖI HOÀN TOÀN
                    const timetable = loadTimetableFromStorage();
                    const weekKey = getWeekKey(currentWeek);
                    const dayKey = `${weekKey}-${dayIndex}`;
                    
                    if (timetable[dayKey]) {
                        const daySchedule = timetable[dayKey];
                        
                        // Tìm tất cả môn học trong ngày này
                        Object.values(daySchedule).forEach(subject => {
                            const subjectStartHour = parseInt(subject.startTime.split(':')[0]);
                            const subjectEndHour = parseInt(subject.endTime.split(':')[0]);
                            
                            // Hiển thị môn học nếu giờ hiện tại nằm trong khoảng thời gian của môn học
                            if (hour >= subjectStartHour && hour < subjectEndHour) {
                                const subjectElement = document.createElement('div');
                                subjectElement.className = `timetable-subject ${subject.priority}`;
                                subjectElement.style.backgroundColor = subject.color;
                                
                                let subjectText = subject.name;
                                if (subject.note) {
                                    subjectText += ' 📝';
                                }
                                
                                // Chỉ hiển thị tên đầy đủ ở giờ đầu tiên
                                if (hour === subjectStartHour) {
                                    subjectElement.textContent = `${subjectText} (${subject.startTime}-${subject.endTime})`;
                                } else {
                                    subjectElement.textContent = subjectText;
                                }
                                
                                let tooltipText = `${subject.name}\n${subject.description || 'Không có mô tả'}\n${subject.startTime}-${subject.endTime}`;
                                if (subject.note) {
                                    tooltipText += `\n\nGhi chú: ${subject.note}`;
                                }
                                subjectElement.title = tooltipText;
                                
                                // Thêm sự kiện xóa khi click chuột phải
                                subjectElement.addEventListener('contextmenu', (e) => {
                                    e.preventDefault();
                                    removeFromTimetable(dayIndex, subject.startTime, weekKey);
                                });
                                
                                cell.appendChild(subjectElement);
                            }
                        });
                    }
                    
                    row.appendChild(cell);
                }
                
                timetableBody.appendChild(row);
            }
        }

        // Lấy key cho tuần hiện tại
        function getWeekKey(weekOffset) {
            const now = new Date();
            const startOfWeek = new Date(now);
            startOfWeek.setDate(now.getDate() - now.getDay() + 1 + (weekOffset * 7)); // Thứ 2 là đầu tuần
            return startOfWeek.toISOString().split('T')[0];
        }

        // Cập nhật hiển thị tuần hiện tại
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

        // Mở modal thêm môn học vào TKB
        function openTimetableModal(day, hour) {
            document.getElementById('timetableDay').value = day;
            
            // Đặt thời gian mặc định dựa trên ô được click
            startTime24h = `${hour.toString().padStart(2, '0')}:00`;
            endTime24h = `${(hour + 1).toString().padStart(2, '0')}:00`;
            
            // Reset phần ghi chú
            document.getElementById('timetableNote').value = '';
            document.getElementById('noteContent').classList.remove('show');
            document.getElementById('notePreview').classList.remove('show');
            document.getElementById('noteToggle').textContent = '+ Thêm ghi chú';
            
            initializeTimeDropdowns();
            document.getElementById('timetableModal').style.display = 'flex';
        }

        // Đóng modal
        function closeTimetableModal() {
            document.getElementById('timetableModal').style.display = 'none';
        }

        // Thêm môn học vào TKB - ĐÃ SỬA LỖI HOÀN TOÀN
        function addToTimetable(event) {
            event.preventDefault();
            
            const subjectSelect = document.getElementById('timetableSubject');
            const subjectId = subjectSelect.value;
            const day = parseInt(document.getElementById('timetableDay').value);
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
            const weekKey = getWeekKey(currentWeek);
            const dayKey = `${weekKey}-${day}`;
            
            if (!timetable[dayKey]) {
                timetable[dayKey] = {};
            }
            
            // Tạo thông tin môn học
            const subjectInfo = {
                id: subjectId,
                name: subjectName,
                description: subjectDescription,
                priority: priority,
                color: color,
                startTime: startTime24h,
                endTime: endTime24h,
                duration: duration.totalMinutes,
                note: note || null
            };
            
            // Sử dụng startTime24h làm key để lưu trữ
            timetable[dayKey][startTime24h] = subjectInfo;
            
            saveTimetableToStorage(timetable);
            generateTimetable(); // Gọi lại để cập nhật hiển thị
            closeTimetableModal();
            
            // Tự động tạo task trong Lịch học nếu được chọn
            if (autoCreateTask) {
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
                
                // Hiển thị thông báo
                showNotification("Thành công", `Đã thêm "${subjectName}" vào TKB và Lịch học`, "success");
            } else {
                showNotification("Thành công", `Đã thêm "${subjectName}" vào TKB`, "success");
            }
            
            // Render lại danh sách task để cập nhật trạng thái
            renderTasks();
        }

        // Thêm nhanh vào TKB
        function quickAddToTimetable(taskId) {
            const tasks = loadTasksFromStorage();
            const task = tasks.find(t => t.id === taskId);
            
            if (!task) return;
            
            // Mở modal TKB và điền thông tin môn học
            document.getElementById('timetableSubject').value = taskId;
            document.getElementById('subjectDescription').value = task.description || '';
            document.getElementById('subjectPriority').value = task.priority;
            document.getElementById('timetableModal').style.display = 'flex';
            
            // Đặt thời gian mặc định (ví dụ: 1 tiếng sau thời gian hiện tại)
            const now = new Date();
            const startHour = now.getHours();
            const startMinute = Math.ceil(now.getMinutes() / 5) * 5; // Làm tròn lên đến 5 phút gần nhất
            
            startTime24h = `${startHour.toString().padStart(2, '0')}:${startMinute.toString().padStart(2, '0')}`;
            
            const endTime = new Date(now.getTime() + 60 * 60 * 1000); // +1 giờ
            const endHour = endTime.getHours();
            const endMinute = endTime.getMinutes();
            
            endTime24h = `${endHour.toString().padStart(2, '0')}:${endMinute.toString().padStart(2, '0')}`;
            
            initializeTimeDropdowns();
        }

        // Xóa môn học khỏi TKB
        function removeFromTimetable(day, timeSlot, weekKey) {
            if (confirm('Bạn có chắc chắn muốn xóa môn học này khỏi thời khóa biểu?')) {
                const timetable = loadTimetableFromStorage();
                const dayKey = `${weekKey}-${day}`;
                
                if (timetable[dayKey] && timetable[dayKey][timeSlot]) {
                    const subjectName = timetable[dayKey][timeSlot].name;
                    delete timetable[dayKey][timeSlot];
                    saveTimetableToStorage(timetable);
                    generateTimetable();
                    
                    // Hiển thị thông báo
                    showNotification("Đã xóa", `Đã xóa "${subjectName}" khỏi TKB`, "info");
                    
                    // Render lại danh sách task
                    renderTasks();
                }
            }
        }

        // Xóa toàn bộ TKB
        function clearTimetable() {
            if (confirm('Bạn có chắc chắn muốn xóa toàn bộ thời khóa biểu?')) {
                saveTimetableToStorage({});
                generateTimetable();
                
                // Hiển thị thông báo
                showNotification("Đã xóa", "Đã xóa toàn bộ thời khóa biểu", "info");
                
                // Render lại danh sách task
                renderTasks();
            }
        }

        // Điền danh sách môn học vào select
        function populateTimetableSubjects() {
            const subjectSelect = document.getElementById('timetableSubject');
            const tasks = loadTasksFromStorage();
            
            // Giữ lại option đầu tiên
            subjectSelect.innerHTML = '<option value="">Chọn môn học</option>';
            
            // Thêm môn học mặc định
            defaultSubjects.forEach(subject => {
                const option = document.createElement('option');
                option.value = subject.id;
                option.textContent = subject.name;
                subjectSelect.appendChild(option);
            });
            
            // Thêm môn học từ danh sách task
            tasks.forEach(task => {
                const option = document.createElement('option');
                option.value = task.id;
                option.textContent = task.name;
                subjectSelect.appendChild(option);
            });
        }

        // Thêm event listeners cho các dropdown
        function setupTimeEventListeners() {
            // Event listeners cho dropdowns
            document.getElementById('startHour').addEventListener('change', updateTimeDisplay);
            document.getElementById('startMinute').addEventListener('change', updateTimeDisplay);
            document.getElementById('endHour').addEventListener('change', updateTimeDisplay);
            document.getElementById('endMinute').addEventListener('change', updateTimeDisplay);
        }

        // Chuyển đổi giữa các tab
        function setupTabs() {
            const tabs = document.querySelectorAll('.tab');
            
            tabs.forEach(tab => {
                tab.addEventListener('click', () => {
                    // Xóa class active từ tất cả các tab và nội dung
                    document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
                    document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
                    
                    // Thêm class active cho tab được click
                    tab.classList.add('active');
                    
                    // Hiển thị nội dung tương ứng
                    const tabId = tab.getAttribute('data-tab');
                    document.getElementById(`${tabId}-tab`).classList.add('active');
                    
                    // Đồng bộ lại dữ liệu khi chuyển tab
                    if (tabId === 'tasks') {
                        setTimeout(renderTasks, 100);
                    } else if (tabId === 'timetable') {
                        setTimeout(generateTimetable, 100);
                    }
                });
            });
        }

        // Cập nhật màu sắc xem trước
        function setupColorPreview() {
            const colorSelect = document.getElementById('timetableColor');
            const colorPreview = document.getElementById('colorPreview');
            
            colorSelect.addEventListener('change', () => {
                colorPreview.style.backgroundColor = colorSelect.value;
            });
        }

        // Chuyển tab từ header
        function switchToTab(tabName) {
            // Xóa class active từ tất cả các tab và nội dung
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
            
            // Thêm class active cho tab được chọn
            document.querySelector(`[data-tab="${tabName}"]`).classList.add('active');
            document.getElementById(`${tabName}-tab`).classList.add('active');
            
            // Đồng bộ lại dữ liệu khi chuyển sang tab tasks
            if (tabName === 'tasks') {
                setTimeout(renderTasks, 100);
            } else if (tabName === 'timetable') {
                setTimeout(generateTimetable, 100);
            }
        }

        // Hiển thị lịch học tuần
        function showWeeklySchedule() {
            const timetable = loadTimetableFromStorage();
            const now = new Date();
            const startOfWeek = new Date(now);
            startOfWeek.setDate(now.getDate() - now.getDay() + 1); // Thứ 2 đầu tuần
            
            let weeklySchedule = {};
            
            // Nhóm môn học theo ngày
            Object.keys(timetable).forEach(dayKey => {
                const daySchedule = timetable[dayKey];
                const dayIndex = parseInt(dayKey.split('-')[1]);
                
                if (!weeklySchedule[dayIndex]) {
                    weeklySchedule[dayIndex] = [];
                }
                
                Object.values(daySchedule).forEach(subject => {
                    weeklySchedule[dayIndex].push({
                        name: subject.name,
                        time: `${subject.startTime}-${subject.endTime}`,
                        description: subject.description
                    });
                });
            });
            
            // Tạo thông báo lịch học tuần
            let scheduleMessage = "";
            const dayNames = ['Chủ nhật', 'Thứ 2', 'Thứ 3', 'Thứ 4', 'Thứ 5', 'Thứ 6', 'Thứ 7'];
            
            Object.keys(weeklySchedule).sort().forEach(dayIndex => {
                const classes = weeklySchedule[dayIndex];
                if (classes.length > 0) {
                    scheduleMessage += `📅 ${dayNames[parseInt(dayIndex)]}:\n`;
                    classes.forEach(cls => {
                        scheduleMessage += `   ⏰ ${cls.time} - ${cls.name}\n`;
                    });
                    scheduleMessage += "\n";
                }
            });
            
            if (scheduleMessage === "") {
                scheduleMessage = "Chưa có lịch học nào trong tuần này.";
            }
            
            showNotification(
                "📚 Lịch học tuần",
                scheduleMessage,
                'info',
                20000
            );
        }

        // Thiết lập đồng bộ hóa real-time
        function setupRealTimeSync() {
            // Đồng bộ khi modal đóng
            document.querySelector('.close-modal').addEventListener('click', function() {
                setTimeout(renderTasks, 100);
            });
        }

        // Khởi tạo ứng dụng
        function initApp() {
            updateCurrentDate();
            renderTasks();
            updateStats();
            
            // Tải cài đặt thông báo
            notificationSettings = loadNotificationSettings();
            
            // Khởi động hệ thống thông báo
            if (notificationSettings.enabled) {
                startNotificationChecker();
            }
            
            // Thêm sự kiện cho form
            document.getElementById('taskForm').addEventListener('submit', addTask);
            
            // Khởi tạo thời khóa biểu
            generateTimetable();
            updateWeekDisplay();
            populateTimetableSubjects();
            initializeTimeDropdowns();
            setupTimeEventListeners();
            setupNoteSection();
            
            // Thêm sự kiện cho TKB
            document.getElementById('timetableForm').addEventListener('submit', addToTimetable);
            document.getElementById('addToTimetable').addEventListener('click', () => openTimetableModal(1, 7));
            document.getElementById('clearTimetable').addEventListener('click', clearTimetable);
            document.querySelector('.close-modal').addEventListener('click', closeTimetableModal);
            document.getElementById('prevWeek').addEventListener('click', () => {
                currentWeek--;
                updateWeekDisplay();
                generateTimetable();
            });
            document.getElementById('nextWeek').addEventListener('click', () => {
                currentWeek++;
                updateWeekDisplay();
                generateTimetable();
            });
            
            // Thiết lập tabs
            setupTabs();
            setupColorPreview();
            
            // Thêm real-time sync
            setupRealTimeSync();
            
            // Cập nhật thời gian mỗi phút
            setInterval(updateCurrentDate, 60000);
            
            // Hiển thị thông báo chào mừng và lịch học tuần
            setTimeout(() => {
                showNotification(
                    "Chào mừng!",
                    "Hệ thống thông báo đã được kích hoạt. Bạn sẽ nhận được thông báo khi sắp đến giờ học.",
                    "info",
                    8000
                );
            }, 2000);
        }

        // Chạy ứng dụng khi trang đã tải xong
        document.addEventListener('DOMContentLoaded', initApp);
    </script>
</body>
</html>
