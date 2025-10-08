<html lang="fr">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chat Application</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <style>
        :root {
            --primary-color: #667eea;
            --primary-dark: #5a6fd8;
            --secondary-color: #764ba2;
            --accent-color: #f093fb;
            --text-primary: #2d3748;
            --text-secondary: #718096;
            --bg-primary: #ffffff;
            --bg-secondary: #f7fafc;
            --border-color: #e2e8f0;
            --success-color: #10b981;
            --warning-color: #f59e0b;
            --error-color: #ef4444;
            --online-color: #10b981;
            --away-color: #f59e0b;
            --busy-color: #ef4444;
            --offline-color: #6b7280;
        }

        [data-theme="dark"] {
            --primary-color: #818cf8;
            --primary-dark: #6366f1;
            --secondary-color: #a78bfa;
            --accent-color: #c084fc;
            --text-primary: #f1f5f9;
            --text-secondary: #cbd5e1;
            --bg-primary: #1e293b;
            --bg-secondary: #0f172a;
            --border-color: #334155;
            --success-color: #34d399;
            --warning-color: #fbbf24;
            --error-color: #f87171;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
            background-color: var(--bg-secondary);
            color: var(--text-primary);
            height: 100vh;
            overflow: hidden;
            transition: all 0.3s ease;
        }

        .app-container {
            display: flex;
            height: 100vh;
            position: relative;
        }

        /* Sidebar */
        .sidebar {
            width: 280px;
            height: 100vh;
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--secondary-color) 100%);
            color: white;
            overflow-y: auto;
            box-shadow: 2px 0 10px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease;
            z-index: 200;
            display: flex;
            flex-direction: column;
        }

        .sidebar-header {
            padding: 20px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            background: rgba(0, 0, 0, 0.1);
        }

        .user-info {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 15px;
        }

        .user-details {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .user-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.2);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            font-size: 16px;
        }

        .user-name {
            font-size: 16px;
            font-weight: bold;
            color: #ecf0f1;
        }

        .user-status {
            font-size: 11px;
            opacity: 0.8;
            margin-top: 3px;
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .status-indicator {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: var(--online-color);
        }

        .status-indicator.away {
            background: var(--away-color);
        }

        .status-indicator.busy {
            background: var(--busy-color);
        }

        .status-indicator.offline {
            background: var(--offline-color);
        }

        .logout-btn {
            background: rgba(255, 255, 255, 0.2);
            color: white;
            border: none;
            padding: 6px 12px;
            border-radius: 15px;
            cursor: pointer;
            font-size: 11px;
            transition: all 0.3s ease;
            backdrop-filter: blur(10px);
        }

        .logout-btn:hover {
            background: rgba(255, 255, 255, 0.3);
            transform: translateY(-1px);
        }

        .sidebar-content {
            padding: 0 20px 20px;
            flex: 1;
            display: flex;
            flex-direction: column;
        }

        .section-title {
            display: block;
            margin: 15px 0;
            color: #ecf0f1;
            font-size: 14px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            padding-bottom: 8px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .user-list {
            flex: 1;
            overflow-y: auto;
        }

        .user-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 10px;
            margin: 5px 0;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
            position: relative;
        }

        .user-item:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: translateX(5px);
        }

        .user-item.active {
            background: rgba(255, 255, 255, 0.25);
            box-shadow: 0 0 0 2px rgba(255, 255, 255, 0.3);
        }

        .user-info-small {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .user-status-small {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: var(--online-color);
            border: 2px solid white;
        }

        .user-status-small.away {
            background: var(--away-color);
        }

        .user-status-small.busy {
            background: var(--busy-color);
        }

        .user-status-small.offline {
            background: var(--offline-color);
        }

        .user-name-small {
            font-size: 13px;
            color: #ecf0f1;
        }

        .notification-badge {
            background: var(--error-color);
            color: white;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            display: none;
            align-items: center;
            justify-content: center;
            font-size: 11px;
            font-weight: bold;
            animation: pulse 1s infinite;
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.1); }
        }

        /* Main Chat Area */
        .main-content {
            flex: 1;
            display: flex;
            flex-direction: column;
            height: 100vh;
            background: var(--bg-primary);
            transition: all 0.3s ease;
        }

        .chat-header {
            height: 70px;
            background: var(--bg-primary);
            border-bottom: 1px solid var(--border-color);
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 0 30px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
            z-index: 150;
        }

        .chat-info {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .chat-title {
            color: var(--text-primary);
            font-size: 18px;
            font-weight: bold;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .private-chat-indicator {
            background: linear-gradient(135deg, var(--secondary-color) 0%, var(--accent-color) 100%);
            color: white;
            padding: 6px 12px;
            border-radius: 20px;
            font-size: 12px;
            display: none;
        }

        .chat-actions {
            display: flex;
            gap: 10px;
            align-items: center;
        }

        .action-btn {
            background: var(--bg-secondary);
            border: 1px solid var(--border-color);
            color: var(--text-primary);
            padding: 8px 15px;
            border-radius: 20px;
            cursor: pointer;
            font-size: 13px;
            font-weight: 600;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .action-btn:hover {
            background: var(--primary-color);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
        }

        .action-btn.active {
            background: var(--primary-color);
            color: white;
        }

        .mobile-menu-btn {
            display: none;
            background: none;
            border: none;
            font-size: 20px;
            color: var(--text-primary);
            cursor: pointer;
            padding: 10px;
        }

        .chat-area {
            flex: 1;
            overflow-y: auto;
            padding: 20px;
            background: var(--bg-secondary);
            scroll-behavior: smooth;
        }

        .message-input-container {
            background: var(--bg-primary);
            border-top: 1px solid var(--border-color);
            padding: 15px 30px;
            box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.05);
        }

        .reply-indicator {
            display: none;
            background: rgba(52, 152, 219, 0.1);
            border-left: 3px solid var(--primary-color);
            padding: 8px 12px;
            border-radius: 5px;
            margin-bottom: 10px;
            font-size: 12px;
            color: var(--text-secondary);
        }

        .reply-close {
            float: right;
            cursor: pointer;
            color: var(--text-secondary);
            font-weight: bold;
        }

        .input-group {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        #message {
            flex: 1;
            height: 45px;
            border: 2px solid var(--border-color);
            border-radius: 22px;
            padding: 0 20px;
            font-size: 14px;
            transition: all 0.3s ease;
            background: var(--bg-primary);
            color: var(--text-primary);
        }

        #message:focus {
            outline: none;
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .send-btn {
            height: 45px;
            padding: 0 18px;
            border: none;
            border-radius: 22px;
            cursor: pointer;
            font-size: 13px;
            font-weight: 600;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            gap: 6px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--secondary-color) 100%);
            color: white;
        }

        .send-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
        }

        .emoji-btn, .attach-btn {
            height: 45px;
            width: 45px;
            border: none;
            border-radius: 50%;
            cursor: pointer;
            font-size: 16px;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            background: var(--bg-secondary);
            color: var(--text-primary);
        }

        .emoji-btn:hover, .attach-btn:hover {
            background: var(--primary-color);
            color: white;
            transform: translateY(-2px);
        }

        /* Messages */
        .message {
            margin-bottom: 15px;
            padding: 12px 16px;
            border-radius: 18px;
            max-width: 70%;
            word-wrap: break-word;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
            position: relative;
            animation: messageSlide 0.3s ease-out;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .message:hover {
            transform: translateY(-1px);
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
        }

        @keyframes messageSlide {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .message.sent {
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--primary-dark) 100%);
            color: white;
            margin-left: auto;
            border-bottom-right-radius: 5px;
        }

        .message.received {
            background: var(--bg-primary);
            color: var(--text-primary);
            margin-right: auto;
            border: 1px solid var(--border-color);
            border-bottom-left-radius: 5px;
        }

        /* Styles spécifiques pour les messages privés */
        .message.private.sent {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            margin-left: auto;
            border-bottom-right-radius: 5px;
        }

        .message.private.received {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            margin-right: auto;
            border-bottom-left-radius: 5px;
        }

        .message.system {
            background: linear-gradient(135deg, #17a2b8 0%, #138496 100%);
            color: white;
            text-align: center;
            margin: 10px auto;
            font-size: 13px;
            max-width: 90%;
        }

        .message-header {
            font-size: 11px;
            opacity: 0.8;
            margin-bottom: 4px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .message-reply {
            background: rgba(255, 255, 255, 0.2);
            border-left: 3px solid rgba(255, 255, 255, 0.5);
            padding: 6px 10px;
            margin-bottom: 8px;
            border-radius: 4px;
            font-size: 11px;
            opacity: 0.9;
        }

        .message.received .message-reply {
            background: rgba(0, 0, 0, 0.05);
            border-left-color: rgba(0, 0, 0, 0.2);
        }

        .message-text {
            font-size: 14px;
            line-height: 1.4;
        }

        .message-actions {
            position: absolute;
            top: -10px;
            right: 10px;
            background: var(--bg-primary);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 5px;
            display: none;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            z-index: 10;
        }

        .message:hover .message-actions {
            display: flex;
            gap: 5px;
        }

        .message-action {
            background: none;
            border: none;
            cursor: pointer;
            padding: 5px;
            border-radius: 4px;
            color: var(--text-secondary);
            transition: all 0.2s ease;
        }

        .message-action:hover {
            background: var(--bg-secondary);
            color: var(--text-primary);
        }

        .message-reactions {
            display: flex;
            gap: 5px;
            margin-top: 8px;
            flex-wrap: wrap;
        }

        .reaction {
            background: var(--bg-secondary);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 2px 6px;
            font-size: 12px;
            display: flex;
            align-items: center;
            gap: 3px;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .reaction:hover {
            background: var(--primary-color);
            color: white;
        }

        .reaction-count {
            font-size: 10px;
        }

        /* Emoji Picker */
        .emoji-picker {
            display: none;
            position: absolute;
            bottom: 80px;
            left: 30px;
            width: 320px;
            height: 200px;
            background: var(--bg-primary);
            border: 1px solid var(--border-color);
            border-radius: 15px;
            padding: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
            z-index: 1000;
            overflow-y: auto;
        }

        .emoji-picker.active {
            display: block;
        }

        .emoji-category {
            margin-bottom: 10px;
        }

        .emoji-category-title {
            font-size: 12px;
            color: var(--text-secondary);
            margin-bottom: 5px;
            padding-bottom: 5px;
            border-bottom: 1px solid var(--border-color);
        }

        .emoji {
            cursor: pointer;
            font-size: 22px;
            margin: 6px;
            display: inline-block;
            transition: transform 0.2s ease;
            padding: 4px;
            border-radius: 6px;
        }

        .emoji:hover {
            transform: scale(1.3);
            background: rgba(102, 126, 234, 0.1);
        }

        /* Auth Screens */
        .auth-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--secondary-color) 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            padding: 20px;
        }

        .auth-box {
            background: var(--bg-primary);
            border-radius: 24px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.15);
            width: 100%;
            max-width: 420px;
            padding: 40px;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .auth-header {
            text-align: center;
            margin-bottom: 30px;
        }

        .auth-title {
            color: var(--primary-color);
            font-weight: 700;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
            margin-bottom: 10px;
            font-size: 1.8rem;
        }

        .auth-subtitle {
            color: var(--text-secondary);
            font-size: 0.9rem;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            color: var(--text-primary);
            font-weight: 600;
            margin-bottom: 8px;
            font-size: 0.9rem;
        }

        .form-input {
            width: 100%;
            padding: 14px 18px;
            border: 2px solid var(--border-color);
            border-radius: 12px;
            font-size: 0.95rem;
            background: var(--bg-primary);
            color: var(--text-primary);
            transition: all 0.3s ease;
            outline: none;
        }

        .form-input:focus {
            border-color: var(--primary-color);
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        .form-input.error {
            border-color: var(--error-color);
        }

        .error-message {
            color: var(--error-color);
            font-size: 0.8rem;
            margin-top: 5px;
            display: none;
        }

        .btn-primary {
            width: 100%;
            padding: 14px;
            background: linear-gradient(135deg, var(--primary-color) 0%, var(--secondary-color) 100%);
            color: white;
            border: none;
            border-radius: 12px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(102, 126, 234, 0.4);
        }

        .auth-switch {
            text-align: center;
            margin-top: 20px;
            font-size: 0.9rem;
            color: var(--text-secondary);
        }

        .auth-link {
            color: var(--primary-color);
            cursor: pointer;
            font-weight: 600;
            transition: all 0.2s ease;
        }

        .auth-link:hover {
            text-decoration: underline;
        }

        /* Notifications */
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 12px 20px;
            border-radius: 8px;
            color: white;
            font-size: 13px;
            font-weight: 600;
            z-index: 9999;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
            transform: translateX(400px);
            transition: all 0.4s ease;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .notification.show {
            transform: translateX(0);
        }

        .notification.info {
            background: linear-gradient(135deg, var(--success-color) 0%, #34d399 100%);
        }

        .notification.warning {
            background: linear-gradient(135deg, var(--warning-color) 0%, #fbbf24 100%);
        }

        .notification.error {
            background: linear-gradient(135deg, var(--error-color) 0%, #f87171 100%);
        }

        /* Search */
        .search-container {
            position: relative;
            margin-bottom: 15px;
        }

        .search-input {
            width: 100%;
            padding: 10px 15px 10px 40px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 20px;
            background: rgba(255, 255, 255, 0.1);
            color: white;
            font-size: 13px;
            transition: all 0.3s ease;
        }

        .search-input:focus {
            outline: none;
            background: rgba(255, 255, 255, 0.2);
            box-shadow: 0 0 0 2px rgba(255, 255, 255, 0.3);
        }

        .search-input::placeholder {
            color: rgba(255, 255, 255, 0.6);
        }

        .search-icon {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: rgba(255, 255, 255, 0.6);
        }

        /* Status Selector */
        .status-selector {
            position: relative;
            display: inline-block;
        }

        .status-dropdown {
            display: none;
            position: absolute;
            top: 100%;
            left: 0;
            background: var(--bg-primary);
            border: 1px solid var(--border-color);
            border-radius: 8px;
            padding: 10px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            z-index: 100;
            min-width: 150px;
        }

        .status-selector:hover .status-dropdown {
            display: block;
        }

        .status-option {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 8px;
            border-radius: 4px;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .status-option:hover {
            background: var(--bg-secondary);
        }

        /* Mobile Responsive */
        @media (max-width: 768px) {
            .sidebar {
                position: fixed;
                transform: translateX(-100%);
                width: 85%;
                max-width: 300px;
                z-index: 300;
            }

            .sidebar.mobile-open {
                transform: translateX(0);
            }

            .main-content {
                width: 100%;
            }

            .chat-header {
                padding: 0 15px;
                height: 60px;
            }

            .chat-title {
                font-size: 16px;
            }

            .mobile-menu-btn {
                display: block;
            }

            .chat-actions {
                gap: 5px;
            }

            .action-btn span {
                display: none;
            }

            .action-btn {
                padding: 8px;
                width: 40px;
                height: 40px;
                justify-content: center;
            }

            .chat-area {
                padding: 15px;
                height: calc(100vh - 140px);
            }

            .message-input-container {
                padding: 10px 15px;
                height: 80px;
            }

            .input-group {
                gap: 8px;
            }

            #message {
                height: 40px;
                font-size: 13px;
                padding: 0 15px;
            }

            .send-btn, .emoji-btn, .attach-btn {
                height: 40px;
                width: 40px;
                padding: 0 12px;
                font-size: 12px;
            }

            .send-btn span {
                display: none;
            }

            .message {
                max-width: 85%;
                padding: 10px 14px;
                font-size: 13px;
            }

            .emoji-picker {
                width: calc(100% - 30px);
                left: 15px;
                bottom: 90px;
            }

            .auth-box {
                margin: 20px;
                max-width: calc(100% - 40px);
                padding: 30px 25px;
            }

            .auth-title {
                font-size: 1.5rem;
            }

            .sidebar-content {
                padding: 0 15px 15px;
            }

            .user-item {
                padding: 8px;
                margin: 3px 0;
            }

            .user-name-small {
                font-size: 12px;
            }

            .sidebar-header {
                padding: 15px;
            }

            .user-name {
                font-size: 14px;
            }

            .logout-btn {
                padding: 5px 10px;
                font-size: 10px;
            }
        }

        @media (max-width: 480px) {
            .message {
                max-width: 90%;
                padding: 8px 12px;
            }

            .message-input-container {
                height: 70px;
            }

            .chat-area {
                height: calc(100vh - 130px);
            }
        }

        /* Mobile Overlay */
        .mobile-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            z-index: 250;
        }

        .mobile-overlay.active {
            display: block;
        }

        /* Theme Toggle */
        .theme-toggle {
            background: none;
            border: none;
            color: var(--text-primary);
            cursor: pointer;
            font-size: 18px;
            padding: 8px;
            border-radius: 50%;
            transition: all 0.3s ease;
        }

        .theme-toggle:hover {
            background: var(--bg-secondary);
        }

        /* Photo Preview */
        #photoPreview {
            display: none;
            margin-bottom: 10px;
            border-radius: 10px;
            max-width: 200px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }

        /* Typing Indicator */
        .typing-indicator {
            display: none;
            padding: 10px 15px;
            font-size: 12px;
            color: var(--text-secondary);
            font-style: italic;
        }

        .typing-indicator.active {
            display: block;
        }
    </style>
</head>

<body>
    <!-- Auth Screens -->
    <div id="authContainer" class="auth-container">
        <div class="auth-box">
            <div class="auth-header">
                <h2 class="auth-title">
                    <i class="fas fa-comments"></i> Chat App
                </h2>
                <p class="auth-subtitle">Connectez-vous pour commencer à discuter</p>
            </div>
            
            <!-- Login Form -->
            <div id="loginForm" class="auth-form active">
                <div class="form-group">
                    <label for="loginEmail">Email</label>
                    <input type="email" id="loginEmail" class="form-input" placeholder="votre@email.com" required>
                    <div class="error-message" id="loginEmailError"></div>
                </div>
                <div class="form-group">
                    <label for="loginPassword">Mot de passe</label>
                    <input type="password" id="loginPassword" class="form-input" placeholder="••••••••" required>
                    <div class="error-message" id="loginPasswordError"></div>
                </div>
                <button id="btnLogin" class="btn-primary">
                    <i class="fas fa-sign-in-alt"></i>
                    Se connecter
                </button>
                <div class="auth-switch">
                    Pas de compte ? <span class="auth-link" id="switchToRegister">S'inscrire</span>
                </div>
            </div>
            
            <!-- Register Form -->
            <div id="registerForm" class="auth-form" style="display: none;">
                <div class="form-group">
                    <label for="registerName">Prénom</label>
                    <input type="text" id="registerName" class="form-input" placeholder="Votre prénom" required>
                    <div class="error-message" id="registerNameError"></div>
                </div>
                <div class="form-group">
                    <label for="registerEmail">Email</label>
                    <input type="email" id="registerEmail" class="form-input" placeholder="votre@email.com" required>
                    <div class="error-message" id="registerEmailError"></div>
                </div>
                <div class="form-group">
                    <label for="registerPassword">Mot de passe</label>
                    <input type="password" id="registerPassword" class="form-input" placeholder="••••••••" required>
                    <div class="error-message" id="registerPasswordError"></div>
                </div>
                <div class="form-group">
                    <label for="registerConfirmPassword">Confirmer le mot de passe</label>
                    <input type="password" id="registerConfirmPassword" class="form-input" placeholder="••••••••" required>
                    <div class="error-message" id="registerConfirmPasswordError"></div>
                </div>
                <button id="btnRegister" class="btn-primary">
                    <i class="fas fa-user-plus"></i>
                    S'inscrire
                </button>
                <div class="auth-switch">
                    Déjà un compte ? <span class="auth-link" id="switchToLogin">Se connecter</span>
                </div>
            </div>
        </div>
    </div>

    <!-- Main App -->
    <div id="appContainer" class="app-container" style="display:none;">
        <!-- Mobile Overlay -->
        <div class="mobile-overlay" id="mobileOverlay"></div>

        <!-- Sidebar -->
        <div class="sidebar" id="sidebar">
            <div class="sidebar-header">
                <div class="user-info">
                    <div class="user-details">
                        <div class="user-avatar" id="userAvatar">U</div>
                        <div>
                            <div class="user-name" id="currentUserName">Utilisateur</div>
                            <div class="user-status">
                                <div class="status-indicator online" id="userStatusIndicator"></div>
                                <span id="userStatusText">En ligne</span>
                            </div>
                        </div>
                    </div>
                    <div class="status-selector">
                        <button class="logout-btn" id="statusToggle">
                            <i class="fas fa-chevron-down"></i>
                        </button>
                        <div class="status-dropdown">
                            <div class="status-option" data-status="online">
                                <div class="status-indicator online"></div>
                                <span>En ligne</span>
                            </div>
                            <div class="status-option" data-status="away">
                                <div class="status-indicator away"></div>
                                <span>Absent</span>
                            </div>
                            <div class="status-option" data-status="busy">
                                <div class="status-indicator busy"></div>
                                <span>Occupé</span>
                            </div>
                            <div class="status-option" data-status="offline">
                                <div class="status-indicator offline"></div>
                                <span>Hors ligne</span>
                            </div>
                        </div>
                    </div>
                </div>
                <p style="font-size: 11px; opacity: 0.8;">BTS Niveau 2 - PERLE</p>
            </div>

            <div class="sidebar-content">
                <div class="search-container">
                    <i class="fas fa-search search-icon"></i>
                    <input type="text" class="search-input" id="searchUsers" placeholder="Rechercher des utilisateurs...">
                </div>

                <strong class="section-title">
                    Utilisateurs connectés 
                    <span id="userCount">(0)</span>
                </strong>
                
                <div class="user-list" id="usersList">
                    <!-- Liste des utilisateurs -->
                </div>
                
                <div class="section-title">
                    Paramètres
                </div>
                
                <div class="settings-options">
                    <div class="user-item" id="toggleTheme">
                        <div class="user-info-small">
                            <i class="fas fa-palette"></i>
                            <div class="user-name-small">Mode sombre</div>
                        </div>
                        <div class="theme-toggle">
                            <i class="fas fa-moon"></i>
                        </div>
                    </div>
                    
                    <div class="user-item" id="logoutBtn">
                        <div class="user-info-small">
                            <i class="fas fa-sign-out-alt"></i>
                            <div class="user-name-small">Déconnexion</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Main Content -->
        <div class="main-content">
            <div class="chat-header">
                <div class="chat-info">
                    <button class="mobile-menu-btn" id="mobileMenuBtn">
                        <i class="fas fa-bars"></i>
                    </button>
                    <h3 class="chat-title" id="chatTitle">
                        <i class="fa-solid fa-comment"></i> 
                        Discussion générale
                    </h3>
                    <div class="private-chat-indicator" id="privateChatIndicator">
                        <i class="fas fa-lock"></i> Chat privé
                    </div>
                </div>
                <div class="chat-actions">
                    <button class="action-btn" id="toggleSearch">
                        <i class="fas fa-search"></i>
                        <span>Recherche</span>
                    </button>
                    <button class="action-btn" id="modeAnonyme">
                        <i class="fas fa-user-secret"></i>
                        <span>Mode anonyme</span>
                    </button>
                    <button class="action-btn" id="clearChat">
                        <i class="fas fa-trash"></i>
                        <span>Effacer</span>
                    </button>
                </div>
            </div>
            
            <div class="chat-area" id="chatArea">
                <div class="typing-indicator" id="typingIndicator">
                    <span id="typingUsers"></span> est en train d'écrire...
                </div>
                
                <img src="" id="photoPreview" style="display: none;">
                
                <div class="emoji-picker" id="emojiPicker">
                    <div class="emoji-category">
                        <div class="emoji-category-title">Visages</div>
                        <span class="emoji">😂</span> <span class="emoji">🤣</span> <span class="emoji">😅</span>
                        <span class="emoji">😉</span> <span class="emoji">😎</span> <span class="emoji">😍</span> 
                        <span class="emoji">🥰</span> <span class="emoji">😘</span> <span class="emoji">🤩</span> 
                        <span class="emoji">😥</span> <span class="emoji">😴</span> <span class="emoji">😪</span>
                        <span class="emoji">🤐</span> <span class="emoji">🙄</span> <span class="emoji">🥱</span>
                        <span class="emoji">😛</span>
                    </div>
                    <div class="emoji-category">
                        <div class="emoji-category-title">Gestes</div>
                        <span class="emoji">☝️</span> <span class="emoji">👏</span> <span class="emoji">🙏</span>
                        <span class="emoji">💪</span> <span class="emoji">👍</span> <span class="emoji">👎</span>
                    </div>
                    <div class="emoji-category">
                        <div class="emoji-category-title">Symboles</div>
                        <span class="emoji">❤️</span> <span class="emoji">🔥</span> <span class="emoji">⭐</span>
                        <span class="emoji">🎉</span> <span class="emoji">🚀</span>
                    </div>
                </div>
            </div>
            
            <div class="message-input-container">
                <div class="reply-indicator" id="replyIndicator">
                    <span id="replyText">Réponse à...</span>
                    <span class="reply-close" id="replyClose">×</span>
                </div>
                <div class="input-group">
                    <button class="attach-btn" id="attachBtn">
                        <i class="fas fa-paperclip"></i>
                    </button>
                    <input type="text" id="message" placeholder="Tapez votre message...">
                    <button class="emoji-btn" id="emojiBtn">
                        <i class="fa-regular fa-face-laugh"></i>
                    </button>
                    <button class="send-btn" id="sendBtn">
                        <i class="fas fa-paper-plane"></i>
                        <span>Envoyer</span>
                    </button>
                </div>
                <input type="file" id="fileInput" accept="image/*" style="display:none;">
            </div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";
        import {
            getFirestore, collection, addDoc, doc, getDoc, getDocs,
            onSnapshot, query, orderBy, updateDoc, setDoc, limit, where,
            deleteDoc, serverTimestamp
        } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore.js";
        import {
            getAuth, signInWithEmailAndPassword, createUserWithEmailAndPassword,
            onAuthStateChanged, updateProfile
        } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-auth.js";

        // Configuration Firebase
        const firebaseConfig = {
            apiKey: "AIzaSyAigx8KtDCEulSWjpu17fnYsrqK7C9o3R8",
            authDomain: "petit-jobs-express.firebaseapp.com",
            projectId: "petit-jobs-express",
            storageBucket: "petit-jobs-express.appspot.com",
            messagingSenderId: "446118780236",
            appId: "1:446118780236:web:08c3a87d56bcd67399c3e9"
        };

        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);
        const auth = getAuth(app);

        // Variables globales
        let currentUser = null;
        let isAnonymous = false;
        let connectedUsers = new Map();
        let currentPrivateChat = null;
        let replyingTo = null;
        let privateChatNotifications = new Map();
        let userStatus = 'online';
        let isDarkMode = false;
        let typingUsers = new Map();
        let typingTimeout = null;

        // Éléments DOM
        const authContainer = document.getElementById('authContainer');
        const appContainer = document.getElementById('appContainer');
        const loginForm = document.getElementById('loginForm');
        const registerForm = document.getElementById('registerForm');
        const btnLogin = document.getElementById('btnLogin');
        const btnRegister = document.getElementById('btnRegister');
        const switchToRegister = document.getElementById('switchToRegister');
        const switchToLogin = document.getElementById('switchToLogin');
        const chatArea = document.getElementById('chatArea');
        const messageInput = document.getElementById('message');
        const sidebar = document.getElementById('sidebar');
        const mobileOverlay = document.getElementById('mobileOverlay');
        const mobileMenuBtn = document.getElementById('mobileMenuBtn');
        const typingIndicator = document.getElementById('typingIndicator');
        const typingUsersSpan = document.getElementById('typingUsers');

        // Fonction pour la connexion automatique
        function checkAutoLogin() {
            const savedUser = localStorage.getItem('currentUser');
            if (savedUser) {
                try {
                    const userData = JSON.parse(savedUser);
                    // Vérifier si les données sont valides
                    if (userData && userData.email && userData.nom) {
                        currentUser = userData;
                        document.getElementById('currentUserName').textContent = userData.nom;
                        document.getElementById('userAvatar').textContent = getInitials(userData.nom);
                        
                        authContainer.style.display = 'none';
                        appContainer.style.display = 'flex';
                        
                        // Gérer les utilisateurs connectés et charger les messages
                        manageConnectedUsers();
                        loadMessages();
                        listenToPrivateNotifications();
                        listenToTyping();
                        
                        showNotification(`Bienvenue de retour ${userData.nom} ! 👋`, 'info');
                        return true;
                    }
                } catch (error) {
                    console.error('Erreur lors de la récupération des données utilisateur:', error);
                    localStorage.removeItem('currentUser');
                }
            }
            return false;
        }

        // Fonctions utilitaires
        function showNotification(text, type = 'info') {
            const existingNotif = document.querySelector('.notification');
            if (existingNotif) existingNotif.remove();

            const notif = document.createElement('div');
            notif.className = `notification ${type}`;
            
            let icon = 'info-circle';
            if (type === 'warning') icon = 'exclamation-triangle';
            if (type === 'error') icon = 'exclamation-circle';
            
            notif.innerHTML = `<i class="fas fa-${icon}"></i> ${text}`;
            document.body.appendChild(notif);

            setTimeout(() => notif.classList.add('show'), 100);
            setTimeout(() => {
                notif.classList.remove('show');
                setTimeout(() => notif.remove(), 400);
            }, 4000);
        }

        function formatTime(timestamp) {
            const date = new Date(timestamp);
            const now = new Date();
            const diff = now - date;
            
            if (diff < 60000) return 'À l\'instant';
            if (diff < 3600000) return `${Math.floor(diff / 60000)} min`;
            if (diff < 86400000) return date.toLocaleTimeString('fr-FR', { hour: '2-digit', minute: '2-digit' });
            return date.toLocaleDateString('fr-FR', { day: '2-digit', month: '2-digit' });
        }

        function scrollToBottom() {
            chatArea.scrollTop = chatArea.scrollHeight;
        }

        function validateEmail(email) {
            const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            return re.test(email);
        }

        function validatePassword(password) {
            return password.length >= 6;
        }

        function getInitials(name) {
            return name.split(' ').map(n => n[0]).join('').toUpperCase();
        }

        // Gestion du thème
        function toggleTheme() {
            isDarkMode = !isDarkMode;
            document.body.setAttribute('data-theme', isDarkMode ? 'dark' : 'light');
            localStorage.setItem('darkMode', isDarkMode);
            
            const themeIcon = document.querySelector('.theme-toggle i');
            themeIcon.className = isDarkMode ? 'fas fa-sun' : 'fas fa-moon';
            
            showNotification(`Mode ${isDarkMode ? 'sombre' : 'clair'} activé`, 'info');
        }

        // Vérifier la préférence de thème
        if (localStorage.getItem('darkMode') === 'true') {
            isDarkMode = true;
            document.body.setAttribute('data-theme', 'dark');
        }

        // Mobile menu toggle
        mobileMenuBtn.addEventListener('click', () => {
            sidebar.classList.toggle('mobile-open');
            mobileOverlay.classList.toggle('active');
        });

        mobileOverlay.addEventListener('click', () => {
            sidebar.classList.remove('mobile-open');
            mobileOverlay.classList.remove('active');
        });

        // Fonction pour créer un message
        function createMessageElement(messageData, isSent = false) {
            const messageDiv = document.createElement('div');
            let messageClass = `message ${isSent ? 'sent' : 'received'}`;
            
            // Appliquer des styles différents pour les messages privés
            if (messageData.isPrivate) {
                messageClass += ' private';
            }
            
            if (messageData.isSystem) {
                messageClass += ' system';
            }
            
            messageDiv.className = messageClass;
            messageDiv.dataset.messageId = messageData.id || Date.now();
            messageDiv.dataset.author = messageData.auteur;
            
            let messageHTML = '';
            
            if (!messageData.isSystem) {
                messageHTML += `<div class="message-header">
                    <span>${messageData.auteur}</span>
                    <span>${formatTime(messageData.timestamp)}</span>
                </div>`;
            }
            
            if (messageData.replyTo) {
                messageHTML += `<div class="message-reply">
                    <strong>${messageData.replyTo.author}:</strong> ${messageData.replyTo.text.substring(0, 50)}${messageData.replyTo.text.length > 50 ? '...' : ''}
                </div>`;
            }
            
            messageHTML += `<div class="message-text">${messageData.text}</div>`;
            
            if (messageData.image) {
                messageHTML += `<img src="${messageData.image}" style="max-width: 100%; border-radius: 8px; margin-top: 8px;">`;
            }
            
            // Ajouter les réactions
            if (messageData.reactions && Object.keys(messageData.reactions).length > 0) {
                messageHTML += `<div class="message-reactions">`;
                for (const [emoji, users] of Object.entries(messageData.reactions)) {
                    messageHTML += `<div class="reaction" data-emoji="${emoji}">
                        <span>${emoji}</span>
                        <span class="reaction-count">${users.length}</span>
                    </div>`;
                }
                messageHTML += `</div>`;
            }
            
            // Ajouter les actions de message (édition, suppression)
            if (isSent && !messageData.isSystem) {
                messageHTML += `<div class="message-actions">
                    <button class="message-action edit-message" title="Modifier">
                        <i class="fas fa-edit"></i>
                    </button>
                    <button class="message-action delete-message" title="Supprimer">
                        <i class="fas fa-trash"></i>
                    </button>
                </div>`;
            }
            
            messageDiv.innerHTML = messageHTML;
            
            // Ajouter event listener pour répondre
            if (!messageData.isSystem) {
                messageDiv.addEventListener('click', (e) => {
                    if (!isSent && !e.target.closest('.message-action')) {
                        replyToMessage(messageData);
                    }
                });
            }
            
            // Ajouter les écouteurs d'événements pour les réactions
            const reactionElements = messageDiv.querySelectorAll('.reaction');
            reactionElements.forEach(reaction => {
                reaction.addEventListener('click', () => {
                    addReaction(messageData, reaction.dataset.emoji);
                });
            });
            
            // Ajouter les écouteurs d'événements pour les actions de message
            if (isSent) {
                const editBtn = messageDiv.querySelector('.edit-message');
                const deleteBtn = messageDiv.querySelector('.delete-message');
                
                editBtn.addEventListener('click', () => {
                    editMessage(messageData);
                });
                
                deleteBtn.addEventListener('click', () => {
                    deleteMessage(messageData);
                });
            }
            
            return messageDiv;
        }

        // Fonction pour ajouter une réaction
        async function addReaction(messageData, emoji) {
            if (!currentUser) return;
            
            try {
                const messageRef = doc(db, currentPrivateChat ? "privateMessages" : "messages", messageData.id);
                const messageDoc = await getDoc(messageRef);
                
                if (messageDoc.exists()) {
                    const data = messageDoc.data();
                    const reactions = data.reactions || {};
                    const userReactions = reactions[emoji] || [];
                    
                    // Vérifier si l'utilisateur a déjà réagi avec cet emoji
                    const userIndex = userReactions.indexOf(currentUser.email);
                    
                    if (userIndex > -1) {
                        // Retirer la réaction
                        userReactions.splice(userIndex, 1);
                        if (userReactions.length === 0) {
                            delete reactions[emoji];
                        }
                    } else {
                        // Ajouter la réaction
                        userReactions.push(currentUser.email);
                        reactions[emoji] = userReactions;
                    }
                    
                    await updateDoc(messageRef, { reactions });
                }
            } catch (error) {
                console.error("Erreur lors de l'ajout de réaction:", error);
                showNotification("Erreur lors de l'ajout de réaction", 'error');
            }
        }

        // Fonction pour éditer un message
        function editMessage(messageData) {
            messageInput.value = messageData.text;
            messageInput.focus();
            
            // Stocker l'ID du message à éditer
            messageInput.dataset.editingMessageId = messageData.id;
            
            showNotification("Modification du message. Appuyez sur Entrée pour sauvegarder.", 'info');
        }

        // Fonction pour supprimer un message
        async function deleteMessage(messageData) {
            if (!confirm("Êtes-vous sûr de vouloir supprimer ce message ?")) return;
            
            try {
                await deleteDoc(doc(db, currentPrivateChat ? "privateMessages" : "messages", messageData.id));
                showNotification("Message supprimé", 'info');
            } catch (error) {
                console.error("Erreur lors de la suppression:", error);
                showNotification("Erreur lors de la suppression du message", 'error');
            }
        }

        // Fonction pour répondre à un message
        function replyToMessage(messageData) {
            replyingTo = {
                id: messageData.id,
                author: messageData.auteur,
                text: messageData.text
            };
            
            const replyIndicator = document.getElementById('replyIndicator');
            const replyText = document.getElementById('replyText');
            
            replyText.textContent = `Réponse à ${messageData.auteur}: ${messageData.text.substring(0, 30)}${messageData.text.length > 30 ? '...' : ''}`;
            replyIndicator.style.display = 'block';
            messageInput.focus();
        }

        // Fermer la réponse
        document.getElementById('replyClose').addEventListener('click', () => {
            replyingTo = null;
            document.getElementById('replyIndicator').style.display = 'none';
        });

        // Fonction pour mettre à jour la liste des utilisateurs
        function updateUsersList() {
            const usersList = document.getElementById('usersList');
            const userCount = document.getElementById('userCount');
            
            usersList.innerHTML = '';
            let onlineCount = 0;
            
            connectedUsers.forEach((userData, userId) => {
                if (userId === currentUser?.email) return; // Ne pas afficher l'utilisateur actuel
                
                onlineCount++;
                const userItem = document.createElement('div');
                userItem.className = 'user-item';
                userItem.dataset.userId = userId;
                
                if (currentPrivateChat === userId) {
                    userItem.classList.add('active');
                }
                
                const notificationCount = privateChatNotifications.get(userId) || 0;
                
                userItem.innerHTML = `
                    <div class="user-info-small">
                        <div class="user-status-small ${userData.status || 'online'}"></div>
                        <div class="user-name-small">${userData.nom}</div>
                    </div>
                    <div class="notification-badge" style="display: ${notificationCount > 0 ? 'flex' : 'none'}">${notificationCount}</div>
                `;
                
                userItem.addEventListener('click', () => {
                    startPrivateChat(userId, userData.nom);
                    // Réinitialiser les notifications pour cet utilisateur
                    privateChatNotifications.set(userId, 0);
                    updateUsersList();
                    
                    // Fermer le menu mobile si ouvert
                    if (window.innerWidth <= 768) {
                        sidebar.classList.remove('mobile-open');
                        mobileOverlay.classList.remove('active');
                    }
                });
                
                usersList.appendChild(userItem);
            });
            
            userCount.textContent = `(${onlineCount + 1})`; // +1 pour l'utilisateur actuel
        }

        // Fonction pour démarrer un chat privé
        function startPrivateChat(userId, userName) {
            currentPrivateChat = userId;
            document.getElementById('chatTitle').innerHTML = `<i class="fas fa-lock"></i> Chat avec ${userName}`;
            document.getElementById('privateChatIndicator').classList.add('active');
            
            // Vider le chat et charger les messages privés
            const messages = chatArea.querySelectorAll('.message');
            messages.forEach(msg => msg.remove());
            
            loadPrivateMessages(userId);
            showNotification(`Chat privé avec ${userName} démarré 🔒`, 'info');
        }

        // Fonction pour revenir au chat général
        function backToGeneralChat() {
            currentPrivateChat = null;
            document.getElementById('chatTitle').innerHTML = `<i class="fa-solid fa-comment"></i> Discussion générale`;
            document.getElementById('privateChatIndicator').classList.remove('active');
            
            // Vider le chat et charger les messages généraux
            const messages = chatArea.querySelectorAll('.message');
            messages.forEach(msg => msg.remove());
            
            loadMessages();
            showNotification('Retour au chat général 💬', 'info');
        }

        // Double clic sur le titre pour revenir au chat général
        document.getElementById('chatTitle').addEventListener('dblclick', () => {
            if (currentPrivateChat) {
                backToGeneralChat();
            }
        });

        // Fonction d'envoi de message
        async function sendMessage() {
            const messageText = messageInput.value.trim();
            const hasImage = document.getElementById('photoPreview').style.display !== 'none';

            if (!messageText && !hasImage) {
                showNotification('Veuillez entrer un message ou sélectionner une image', 'error');
                return;
            }

            if (!currentUser) {
                showNotification('Veuillez vous connecter d\'abord', 'error');
                return;
            }

            try {
                const messageData = {
                    auteur: isAnonymous ? 'Anonyme' : currentUser.nom,
                    text: messageText,
                    timestamp: Date.now(),
                    userId: currentUser.email,
                    isAnonymous: isAnonymous,
                    isPrivate: !!currentPrivateChat,
                    recipientId: currentPrivateChat || null
                };

                // Vérifier si on est en mode édition
                const editingMessageId = messageInput.dataset.editingMessageId;
                if (editingMessageId) {
                    // Mettre à jour le message existant
                    const messageRef = doc(db, currentPrivateChat ? "privateMessages" : "messages", editingMessageId);
                    await updateDoc(messageRef, {
                        text: messageText,
                        edited: true,
                        editTimestamp: Date.now()
                    });
                    
                    delete messageInput.dataset.editingMessageId;
                    showNotification('Message modifié ✅', 'info');
                } else {
                    // Créer un nouveau message
                    if (hasImage) {
                        messageData.image = document.getElementById('photoPreview').src;
                    }

                    if (replyingTo) {
                        messageData.replyTo = replyingTo;
                    }

                    // Choisir la collection appropriée
                    const collectionName = currentPrivateChat ? "privateMessages" : "messages";
                    await addDoc(collection(db, collectionName), messageData);
                    showNotification('Message envoyé ! ✅', 'info');
                }
                
                // Réinitialiser les champs
                messageInput.value = '';
                document.getElementById('photoPreview').style.display = 'none';
                document.getElementById('photoPreview').src = '';
                replyingTo = null;
                document.getElementById('replyIndicator').style.display = 'none';
                
            } catch (error) {
                console.error("Erreur envoi message:", error);
                showNotification("Erreur lors de l'envoi du message", 'error');
            }
        }

        // Fonction pour charger les messages généraux
        function loadMessages() {
            const messagesQuery = query(
                collection(db, "messages"), 
                orderBy("timestamp", "asc"),
                limit(50)
            );

            onSnapshot(messagesQuery, (snapshot) => {
                snapshot.docChanges().forEach((change) => {
                    if (change.type === "added" && !currentPrivateChat) {
                        const messageData = { ...change.doc.data(), id: change.doc.id };
                        
                        // Ne pas afficher si c'est un message privé
                        if (messageData.isPrivate) return;
                        
                        const isSent = auth.currentUser && messageData.userId === auth.currentUser.email;
                        const messageElement = createMessageElement(messageData, isSent);
                        
                        // Insérer avant les éléments de contrôle
                        const controlElements = chatArea.querySelectorAll('#photoPreview, .emoji-picker');
                        if (controlElements.length > 0) {
                            chatArea.insertBefore(messageElement, controlElements[0]);
                        } else {
                            chatArea.appendChild(messageElement);
                        }
                        
                        scrollToBottom();
                    }
                });
            });
        }

        // Fonction pour charger les messages privés
        function loadPrivateMessages(userId) {
            const messagesQuery = query(
                collection(db, "privateMessages"),
                orderBy("timestamp", "asc"),
                limit(50)
            );

            onSnapshot(messagesQuery, (snapshot) => {
                const existingMessageIds = new Set();
                const existingMessages = chatArea.querySelectorAll('.message');
                existingMessages.forEach(msg => {
                    if (msg.dataset.messageId) {
                        existingMessageIds.add(msg.dataset.messageId);
                    }
                });

                snapshot.docChanges().forEach((change) => {
                    if (change.type === "added") {
                        const messageData = { ...change.doc.data(), id: change.doc.id };
                        
                        // Vérifier si le message n'existe pas déjà
                        if (existingMessageIds.has(messageData.id)) return;
                        
                        // Afficher seulement les messages entre l'utilisateur actuel et l'utilisateur sélectionné
                        const isConversationMessage = 
                            (messageData.userId === currentUser?.email && messageData.recipientId === userId) ||
                            (messageData.recipientId === currentUser?.email && messageData.userId === userId);
                        
                        if (isConversationMessage) {
                            const isSent = messageData.userId === currentUser?.email;
                            const messageElement = createMessageElement(messageData, isSent);
                            messageElement.dataset.messageId = messageData.id;
                            
                            const controlElements = chatArea.querySelectorAll('#photoPreview, .emoji-picker');
                            if (controlElements.length > 0) {
                                chatArea.insertBefore(messageElement, controlElements[0]);
                            } else {
                                chatArea.appendChild(messageElement);
                            }
                            
                            scrollToBottom();
                        }
                    }
                });
            });
        }

        // Fonction pour écouter les notifications de messages privés
        function listenToPrivateNotifications() {
            onSnapshot(query(collection(db, "privateMessages"), orderBy("timestamp", "asc")), (snapshot) => {
                snapshot.docChanges().forEach((change) => {
                    if (change.type === "added") {
                        const messageData = change.doc.data();
                        
                        // Si c'est un message privé pour l'utilisateur actuel et qu'il n'est pas dans ce chat
                        if (messageData.recipientId === currentUser?.email && 
                            messageData.userId !== currentUser?.email &&
                            currentPrivateChat !== messageData.userId) {
                            
                            // Incrémenter les notifications
                            const currentCount = privateChatNotifications.get(messageData.userId) || 0;
                            privateChatNotifications.set(messageData.userId, currentCount + 1);
                            updateUsersList();
                            
                            showNotification(`Nouveau message privé de ${messageData.auteur} 💌`, 'info');
                        }
                    }
                });
            });
        }

        // Fonction pour gérer les utilisateurs connectés
        function manageConnectedUsers() {
            if (!currentUser) return;

            // Ajouter l'utilisateur actuel à la liste
            const userRef = doc(db, "connectedUsers", currentUser.email);
            setDoc(userRef, {
                nom: currentUser.nom,
                email: currentUser.email,
                lastSeen: Date.now(),
                isOnline: true,
                status: userStatus
            });

            // Écouter les changements d'utilisateurs connectés
            onSnapshot(collection(db, "connectedUsers"), (snapshot) => {
                const previousUsers = new Set(connectedUsers.keys());
                connectedUsers.clear();

                snapshot.forEach((doc) => {
                    const userData = doc.data();
                    const userId = doc.id;
                    
                    // Considérer comme en ligne si vu dans les 30 dernières secondes
                    if (Date.now() - userData.lastSeen < 30000) {
                        connectedUsers.set(userId, userData);
                        
                        // Si c'est un nouvel utilisateur
                        if (!previousUsers.has(userId) && userId !== currentUser.email) {
                            addSystemMessage(`${userData.nom} a rejoint le chat 👋`);
                        }
                    }
                });

                updateUsersList();
            });

            // Mettre à jour la présence toutes les 15 secondes
            setInterval(() => {
                if (currentUser) {
                    updateDoc(doc(db, "connectedUsers", currentUser.email), {
                        lastSeen: Date.now(),
                        status: userStatus
                    });
                }
            }, 15000);
        }

        // Fonction pour ajouter un message système
        function addSystemMessage(text) {
            if (currentPrivateChat) return; // Ne pas afficher dans les chats privés

            const systemMessage = {
                text: text,
                timestamp: Date.now(),
                isSystem: true,
                auteur: 'Système'
            };

            const messageElement = createMessageElement(systemMessage, false);
            
            const controlElements = chatArea.querySelectorAll('#photoPreview, .emoji-picker');
            if (controlElements.length > 0) {
                chatArea.insertBefore(messageElement, controlElements[0]);
            } else {
                chatArea.appendChild(messageElement);
            }
            
            scrollToBottom();
        }

        // Gestion de la connexion
        btnLogin.addEventListener('click', async function() {
            const email = document.getElementById('loginEmail').value.trim();
            const password = document.getElementById('loginPassword').value;

            // Validation des champs
            let hasError = false;
            
            if (!email) {
                document.getElementById('loginEmailError').textContent = "L'email est requis";
                document.getElementById('loginEmailError').style.display = 'block';
                document.getElementById('loginEmail').classList.add('error');
                hasError = true;
            } else if (!validateEmail(email)) {
                document.getElementById('loginEmailError').textContent = "Format d'email invalide";
                document.getElementById('loginEmailError').style.display = 'block';
                document.getElementById('loginEmail').classList.add('error');
                hasError = true;
            } else {
                document.getElementById('loginEmailError').style.display = 'none';
                document.getElementById('loginEmail').classList.remove('error');
            }
            
            if (!password) {
                document.getElementById('loginPasswordError').textContent = "Le mot de passe est requis";
                document.getElementById('loginPasswordError').style.display = 'block';
                document.getElementById('loginPassword').classList.add('error');
                hasError = true;
            } else {
                document.getElementById('loginPasswordError').style.display = 'none';
                document.getElementById('loginPassword').classList.remove('error');
            }
            
            if (hasError) return;

            btnLogin.disabled = true;
            btnLogin.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Connexion...';

            try {
                const userCredential = await signInWithEmailAndPassword(auth, email, password);
                const user = userCredential.user;
                
                // Récupérer les informations utilisateur
                const userDoc = await getDoc(doc(db, "users", user.email));
                if (userDoc.exists()) {
                    const userData = userDoc.data();
                    currentUser = { nom: userData.nom, email: user.email };
                    
                    // Sauvegarder les informations utilisateur pour la connexion automatique
                    localStorage.setItem('currentUser', JSON.stringify(currentUser));
                    
                    document.getElementById('currentUserName').textContent = userData.nom;
                    document.getElementById('userAvatar').textContent = getInitials(userData.nom);
                    
                    authContainer.style.display = 'none';
                    appContainer.style.display = 'flex';
                    
                    // Gérer les utilisateurs connectés et charger les messages
                    manageConnectedUsers();
                    loadMessages();
                    listenToPrivateNotifications();
                    listenToTyping();
                    
                    showNotification(`Bienvenue ${userData.nom} ! 🎉`, 'info');
                } else {
                    throw new Error("Données utilisateur non trouvées");
                }
                
            } catch (error) {
                console.error('Erreur de connexion:', error);
                let errorMessage = 'Erreur lors de la connexion';
                
                if (error.code === 'auth/user-not-found') {
                    errorMessage = "Aucun compte trouvé avec cet email";
                } else if (error.code === 'auth/wrong-password') {
                    errorMessage = "Mot de passe incorrect";
                } else if (error.code === 'auth/invalid-email') {
                    errorMessage = "Adresse email invalide";
                }
                
                showNotification(errorMessage, 'error');
            } finally {
                btnLogin.disabled = false;
                btnLogin.innerHTML = '<i class="fas fa-sign-in-alt"></i> Se connecter';
            }
        });

        // Gestion de l'inscription
        btnRegister.addEventListener('click', async function() {
            const name = document.getElementById('registerName').value.trim();
            const email = document.getElementById('registerEmail').value.trim();
            const password = document.getElementById('registerPassword').value;
            const confirmPassword = document.getElementById('registerConfirmPassword').value;

            // Validation des champs
            let hasError = false;
            
            if (!name) {
                document.getElementById('registerNameError').textContent = "Le nom est requis";
                document.getElementById('registerNameError').style.display = 'block';
                document.getElementById('registerName').classList.add('error');
                hasError = true;
            } else if (name.length < 2) {
                document.getElementById('registerNameError').textContent = "Le nom doit contenir au moins 2 caractères";
                document.getElementById('registerNameError').style.display = 'block';
                document.getElementById('registerName').classList.add('error');
                hasError = true;
            } else {
                document.getElementById('registerNameError').style.display = 'none';
                document.getElementById('registerName').classList.remove('error');
            }
            
            if (!email) {
                document.getElementById('registerEmailError').textContent = "L'email est requis";
                document.getElementById('registerEmailError').style.display = 'block';
                document.getElementById('registerEmail').classList.add('error');
                hasError = true;
            } else if (!validateEmail(email)) {
                document.getElementById('registerEmailError').textContent = "Format d'email invalide";
                document.getElementById('registerEmailError').style.display = 'block';
                document.getElementById('registerEmail').classList.add('error');
                hasError = true;
            } else {
                document.getElementById('registerEmailError').style.display = 'none';
                document.getElementById('registerEmail').classList.remove('error');
            }
            
            if (!password) {
                document.getElementById('registerPasswordError').textContent = "Le mot de passe est requis";
                document.getElementById('registerPasswordError').style.display = 'block';
                document.getElementById('registerPassword').classList.add('error');
                hasError = true;
            } else if (!validatePassword(password)) {
                document.getElementById('registerPasswordError').textContent = "Le mot de passe doit contenir au moins 6 caractères";
                document.getElementById('registerPasswordError').style.display = 'block';
                document.getElementById('registerPassword').classList.add('error');
                hasError = true;
            } else {
                document.getElementById('registerPasswordError').style.display = 'none';
                document.getElementById('registerPassword').classList.remove('error');
            }
            
            if (!confirmPassword) {
                document.getElementById('registerConfirmPasswordError').textContent = "Veuillez confirmer le mot de passe";
                document.getElementById('registerConfirmPasswordError').style.display = 'block';
                document.getElementById('registerConfirmPassword').classList.add('error');
                hasError = true;
            } else if (password !== confirmPassword) {
                document.getElementById('registerConfirmPasswordError').textContent = "Les mots de passe ne correspondent pas";
                document.getElementById('registerConfirmPasswordError').style.display = 'block';
                document.getElementById('registerConfirmPassword').classList.add('error');
                hasError = true;
            } else {
                document.getElementById('registerConfirmPasswordError').style.display = 'none';
                document.getElementById('registerConfirmPassword').classList.remove('error');
            }
            
            if (hasError) return;

            btnRegister.disabled = true;
            btnRegister.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Inscription...';

            try {
                const userCredential = await createUserWithEmailAndPassword(auth, email, password);
                const user = userCredential.user;
                
                // Sauvegarder les informations utilisateur
                await setDoc(doc(db, "users", user.email), {
                    nom: name,
                    email: email,
                    dateCreation: Date.now()
                });
                
                currentUser = { nom: name, email: user.email };
                
                // Sauvegarder les informations utilisateur pour la connexion automatique
                localStorage.setItem('currentUser', JSON.stringify(currentUser));
                
                document.getElementById('currentUserName').textContent = name;
                document.getElementById('userAvatar').textContent = getInitials(name);
                
                authContainer.style.display = 'none';
                appContainer.style.display = 'flex';
                
                // Gérer les utilisateurs connectés et charger les messages
                manageConnectedUsers();
                loadMessages();
                listenToPrivateNotifications();
                listenToTyping();
                
                showNotification(`Compte créé avec succès, bienvenue ${name} ! 🎉`, 'info');
                
            } catch (error) {
                console.error('Erreur d\'inscription:', error);
                let errorMessage = 'Erreur lors de l\'inscription';
                
                if (error.code === 'auth/email-already-in-use') {
                    errorMessage = "Cette adresse email est déjà utilisée";
                } else if (error.code === 'auth/weak-password') {
                    errorMessage = "Le mot de passe est trop faible";
                } else if (error.code === 'auth/invalid-email') {
                    errorMessage = "Adresse email invalide";
                }
                
                showNotification(errorMessage, 'error');
            } finally {
                btnRegister.disabled = false;
                btnRegister.innerHTML = '<i class="fas fa-user-plus"></i> S\'inscrire';
            }
        });

        // Basculer entre les formulaires de connexion et d'inscription
        switchToRegister.addEventListener('click', () => {
            loginForm.style.display = 'none';
            registerForm.style.display = 'block';
        });

        switchToLogin.addEventListener('click', () => {
            registerForm.style.display = 'none';
            loginForm.style.display = 'block';
        });

        // Gestion de la déconnexion
        document.getElementById('logoutBtn').addEventListener('click', async function() {
            try {
                // Marquer comme déconnecté
                if (currentUser) {
                    await updateDoc(doc(db, "connectedUsers", currentUser.email), {
                        isOnline: false,
                        lastSeen: Date.now()
                    });
                }
                
                await auth.signOut();
                
                // Supprimer les données de connexion automatique
                localStorage.removeItem('currentUser');
                
                showNotification('Vous avez été déconnecté avec succès ! 👋', 'info');
                authContainer.style.display = 'flex';
                appContainer.style.display = 'none';
                chatArea.innerHTML = '';
                currentUser = null;
                currentPrivateChat = null;
                connectedUsers.clear();
                privateChatNotifications.clear();
                
                // Réinitialiser les formulaires
                document.getElementById('loginEmail').value = '';
                document.getElementById('loginPassword').value = '';
                document.getElementById('registerName').value = '';
                document.getElementById('registerEmail').value = '';
                document.getElementById('registerPassword').value = '';
                document.getElementById('registerConfirmPassword').value = '';
                
                // Afficher le formulaire de connexion par défaut
                loginForm.style.display = 'block';
                registerForm.style.display = 'none';
            } catch (error) {
                console.error('Erreur lors de la déconnexion:', error);
                showNotification('Erreur lors de la déconnexion', 'error');
            }
        });

        // Gestion du statut utilisateur
        document.querySelectorAll('.status-option').forEach(option => {
            option.addEventListener('click', () => {
                userStatus = option.dataset.status;
                document.getElementById('userStatusIndicator').className = `status-indicator ${userStatus}`;
                
                let statusText = 'En ligne';
                if (userStatus === 'away') statusText = 'Absent';
                if (userStatus === 'busy') statusText = 'Occupé';
                if (userStatus === 'offline') statusText = 'Hors ligne';
                
                document.getElementById('userStatusText').textContent = statusText;
                
                // Mettre à jour le statut dans Firebase
                if (currentUser) {
                    updateDoc(doc(db, "connectedUsers", currentUser.email), {
                        status: userStatus
                    });
                }
                
                showNotification(`Statut changé en "${statusText}"`, 'info');
            });
        });

        // Mode anonyme
        document.getElementById('modeAnonyme').addEventListener('click', function() {
            isAnonymous = !isAnonymous;
            const btn = this;
            if (isAnonymous) {
                btn.innerHTML = '<i class="fas fa-user"></i> <span>Mode normal</span>';
                btn.classList.add('active');
                showNotification('Mode anonyme activé 🥸', 'info');
            } else {
                btn.innerHTML = '<i class="fas fa-user-secret"></i> <span>Mode anonyme</span>';
                btn.classList.remove('active');
                showNotification('Mode normal activé 👤', 'info');
            }
        });

        // Gestion des images
        document.getElementById('attachBtn').addEventListener('click', () => {
            document.getElementById('fileInput').click();
        });
        
        document.getElementById('fileInput').addEventListener('change', function(e) {
            const file = e.target.files[0];
            if (!file) return;

            // Vérifier la taille du fichier (max 5MB)
            if (file.size > 5 * 1024 * 1024) {
                showNotification('L\'image est trop volumineuse (max 5MB)', 'error');
                return;
            }

            const reader = new FileReader();
            reader.onload = function() {
                document.getElementById('photoPreview').src = reader.result;
                document.getElementById('photoPreview').style.display = 'block';
                showNotification('Image sélectionnée ! 📸', 'info');
            };
            reader.readAsDataURL(file);
        });

        // Gestion des emojis
        document.getElementById('emojiBtn').addEventListener('click', function() {
            const emojiPicker = document.getElementById('emojiPicker');
            emojiPicker.classList.toggle('active');
        });

        document.querySelectorAll('.emoji').forEach(emoji => {
            emoji.addEventListener('click', function() {
                messageInput.value += emoji.textContent;
                document.getElementById('emojiPicker').classList.remove('active');
                messageInput.focus();
            });
        });

        // Fermer les emojis en cliquant ailleurs
        document.addEventListener('click', function(e) {
            if (!e.target.closest('#emojiBtn') && !e.target.closest('.emoji-picker')) {
                document.getElementById('emojiPicker').classList.remove('active');
            }
        });

        // Events
        document.getElementById('sendBtn').addEventListener('click', sendMessage);

        messageInput.addEventListener('keypress', function(e) {
            if (e.key === 'Enter' && !e.shiftKey) {
                e.preventDefault();
                sendMessage();
            }
        });

        // Gestion du thème
        document.getElementById('toggleTheme').addEventListener('click', toggleTheme);

        // Effacer le chat
        document.getElementById('clearChat').addEventListener('click', function() {
            if (confirm("Êtes-vous sûr de vouloir effacer tous les messages de cette conversation ?")) {
                const messages = chatArea.querySelectorAll('.message');
                messages.forEach(msg => msg.remove());
                showNotification('Conversation effacée', 'info');
            }
        });

        // Recherche d'utilisateurs
        document.getElementById('searchUsers').addEventListener('input', function(e) {
            const searchTerm = e.target.value.toLowerCase();
            const userItems = document.querySelectorAll('.user-item');
            
            userItems.forEach(item => {
                const userName = item.querySelector('.user-name-small').textContent.toLowerCase();
                if (userName.includes(searchTerm)) {
                    item.style.display = 'flex';
                } else {
                    item.style.display = 'none';
                }
            });
        });

        // Indicateur de frappe
        messageInput.addEventListener('input', function() {
            if (!currentUser || !currentPrivateChat) return;
            
            // Indiquer que l'utilisateur est en train de taper
            const typingRef = doc(db, "typing", currentPrivateChat);
            setDoc(typingRef, {
                userId: currentUser.email,
                userName: currentUser.nom,
                timestamp: Date.now()
            });
            
            // Effacer le timeout existant
            if (typingTimeout) clearTimeout(typingTimeout);
            
            // Définir un nouveau timeout pour arrêter l'indication de frappe
            typingTimeout = setTimeout(() => {
                deleteDoc(typingRef);
            }, 3000);
        });

        // Écouter les indications de frappe
        function listenToTyping() {
            onSnapshot(collection(db, "typing"), (snapshot) => {
                const typingUsersList = [];
                
                snapshot.forEach((doc) => {
                    const typingData = doc.data();
                    
                    // Vérifier si c'est pour la conversation actuelle
                    if (doc.id === currentPrivateChat && typingData.userId !== currentUser.email) {
                        // Vérifier si c'est récent (moins de 3 secondes)
                        if (Date.now() - typingData.timestamp < 3000) {
                            typingUsersList.push(typingData.userName);
                        }
                    }
                });
                
                if (typingUsersList.length > 0) {
                    typingUsersSpan.textContent = typingUsersList.join(', ');
                    typingIndicator.classList.add('active');
                } else {
                    typingIndicator.classList.remove('active');
                }
            });
        }

        // Notification de bienvenue
        setTimeout(() => {
            showNotification("Bienvenue dans BTS Niveau 2 de la PERLE ❤️", "info");
        }, 1000);

        // Messages de bienvenue automatiques
        setTimeout(() => {
            if (currentUser && !currentPrivateChat) {
                addSystemMessage("👋 Bienvenue ! Cliquez sur un utilisateur pour discuter en privé");
            }
        }, 3000);

        // Vérifier la connexion automatique au chargement de la page
        document.addEventListener('DOMContentLoaded', function() {
            if (!checkAutoLogin()) {
                // Si pas de connexion automatique, afficher l'écran d'authentification
                authContainer.style.display = 'flex';
                appContainer.style.display = 'none';
            }
        });

        // Initialiser l'écoute des indications de frappe
        listenToTyping();
    </script>
</body>
