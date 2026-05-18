# https-gemini.google.com-share-fb4ebb9c122c
theme: jekyll-theme-minimal
title: 予約管理アプリ
description: 店舗・サロン・個人事業向けのシンプルな予約管理システム
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>予約管理システム - AIアシスタント搭載</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Noto+Sans+JP:wght@400;500;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        body {
            font-family: 'Inter', 'Noto Sans JP', sans-serif;
            background-color: #f8fafc;
        }
        /* スクロールバーのカスタマイズ */
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9; 
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1; 
            border-radius: 9999px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8; 
        }
        
        /* 輝くAIエフェクト用のカスタムCSS */
        .ai-gradient-text {
            background: linear-gradient(135deg, #6366f1 0%, #a855f7 50%, #ec4899 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .ai-gradient-bg {
            background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 50%, #d946ef 100%);
        }
        .ai-glow {
            box-shadow: 0 0 15px rgba(139, 92, 246, 0.2);
            border: 1px solid rgba(139, 92, 246, 0.3);
        }
        .ai-glow-focus:focus-within {
            box-shadow: 0 0 15px rgba(139, 92, 246, 0.4);
            border-color: rgba(139, 92, 246, 0.6);
        }
        @keyframes pulse-gentle {
            0%, 100% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.85; transform: scale(0.98); }
        }
        .pulse-ai {
            animation: pulse-gentle 3s infinite ease-in-out;
        }
    </style>
</head>
<body class="text-slate-800 h-screen flex flex-col overflow-hidden">

    <!-- ヘッダー -->
    <header class="bg-white border-b border-slate-200 z-10 relative">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16 items-center">
                <div class="flex items-center space-x-3">
                    <div class="bg-gradient-to-tr from-blue-600 to-indigo-600 text-white p-2.5 rounded-xl shadow-md shadow-blue-100 flex items-center justify-center">
                        <i class="fa-regular fa-calendar-check text-xl"></i>
                    </div>
                    <div>
                        <h1 class="font-bold text-lg text-slate-900 tracking-tight flex items-center gap-2">
                            <span>予約管理システム</span>
                            <span class="text-xs font-semibold bg-indigo-50 text-indigo-700 border border-indigo-200 px-2 py-0.5 rounded-full flex items-center gap-1">
                                <i class="fa-solid fa-wand-magic-sparkles text-[10px] ai-gradient-text"></i> AI Assistant
                            </span>
                        </h1>
                        <p class="text-xs text-slate-500 hidden sm:block">飲食店・サロン向け次世代コパイロットシステム</p>
                    </div>
                </div>
                <div class="flex items-center space-x-2">
                    <!-- データ管理ボタン -->
                    <button id="dataManagementBtn" class="bg-white hover:bg-slate-50 text-slate-700 border border-slate-200 font-medium py-2 px-3.5 rounded-xl shadow-sm transition duration-150 flex items-center text-sm gap-2">
                        <i class="fa-solid fa-database text-indigo-500"></i>
                        <span class="hidden sm:inline">データ管理</span>
                    </button>
                    <!-- AIアドバイザー起動ボタン -->
                    <button id="aiAdvisorBtn" class="bg-white hover:bg-slate-50 text-slate-700 border border-slate-200 font-medium py-2 px-3.5 rounded-xl shadow-sm transition duration-150 flex items-center text-sm gap-2">
                        <i class="fa-solid fa-brain ai-gradient-text"></i>
                        <span class="hidden sm:inline">AI予約分析</span>
                    </button>
                    <!-- 新規予約登録ボタン -->
                    <button id="openModalBtn" class="bg-slate-900 hover:bg-slate-800 text-white font-medium py-2 px-4 rounded-xl shadow-sm transition duration-150 flex items-center text-sm gap-2">
                        <i class="fa-solid fa-plus text-xs"></i> <span>新規予約</span>
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- メインコンテンツエリア -->
    <main class="flex-1 flex overflow-hidden">
        
        <!-- 左側：予約一覧パネル -->
        <aside class="w-full md:w-80 lg:w-96 bg-white border-r border-slate-200 flex flex-col overflow-hidden hidden md:flex">
            <!-- 上部：統計情報 & AIサマリートリガー -->
            <div class="p-4 border-b border-slate-200 bg-slate-50">
                <div class="flex justify-between items-center mb-3">
                    <h2 class="font-bold text-slate-800 text-sm tracking-wide uppercase">今日の予約リスト</h2>
                    <span id="todayDate" class="text-xs font-medium text-slate-500"></span>
                </div>
                
                <!-- AI状況サマリーカード -->
                <div id="aiSummaryBanner" class="bg-gradient-to-r from-indigo-50 to-purple-50 rounded-xl p-3 border border-indigo-100 relative overflow-hidden cursor-pointer hover:shadow-sm transition-all duration-200" onclick="triggerDailySummary()">
                    <div class="absolute right-0 bottom-0 opacity-10 transform translate-x-1 translate-y-1">
                        <i class="fa-solid fa-wand-magic-sparkles text-7xl text-indigo-600"></i>
                    </div>
                    <div class="flex items-start gap-2.5">
                        <div class="mt-0.5 bg-indigo-100 rounded-lg p-1.5 flex items-center justify-center">
                            <i class="fa-solid fa-sparkles text-indigo-600 text-xs"></i>
                        </div>
                        <div class="flex-1">
                            <h3 class="text-xs font-bold text-indigo-900 flex items-center gap-1.5">
                                AIアシスタントの分析
                                <span class="inline-block w-2 h-2 rounded-full bg-indigo-500 animate-ping"></span>
                            </h3>
                            <p id="aiSummaryText" class="text-xs text-indigo-700 mt-1 line-clamp-2 leading-relaxed">
                                今日の予約件数や注意事項をAIがスピード分析。クリックして詳細レポートをチェック。
                            </p>
                        </div>
                    </div>
                </div>
            </div>
            
            <!-- 検索フィルター -->
            <div class="p-3.5 border-b border-slate-100">
                <div class="relative">
                    <input type="text" id="searchInput" placeholder="名前や電話番号で検索..." class="w-full pl-9 pr-3 py-2 border border-slate-200 rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-transparent transition-all">
                    <i class="fa-solid fa-search absolute left-3 top-3 text-slate-400 text-sm"></i>
                </div>
            </div>

            <!-- 予約リスト（スクロール可能） -->
            <div id="reservationList" class="flex-1 overflow-y-auto p-3 space-y-2.5">
                <div class="flex justify-center items-center h-full text-slate-400 text-sm">
                    <i class="fa-solid fa-spinner animate-spin mr-2"></i> 読み込み中...
                </div>
            </div>
        </aside>

        <!-- 右側：メインビュー（カレンダー） -->
        <section class="flex-1 flex flex-col bg-slate-50 overflow-hidden relative">
            
            <!-- カレンダーコントロール -->
            <div class="p-4 bg-white border-b border-slate-200 flex justify-between items-center shadow-sm z-0">
                <div class="flex items-center space-x-3">
                    <h2 id="currentMonthYear" class="text-lg font-bold text-slate-800 w-44 tracking-tight">2026年 5月</h2>
                    <div class="flex bg-slate-100 rounded-xl p-0.5 border border-slate-200">
                        <button id="prevMonthBtn" class="p-1.5 px-3 hover:bg-white rounded-lg text-slate-600 hover:text-slate-800 transition duration-150">
                            <i class="fa-solid fa-chevron-left text-xs"></i>
                        </button>
                        <button id="todayBtn" class="px-3 py-1 bg-white shadow-sm rounded-lg text-slate-700 font-semibold text-xs hover:bg-white/90 transition duration-150">
                            今日
                        </button>
                        <button id="nextMonthBtn" class="p-1.5 px-3 hover:bg-white rounded-lg text-slate-600 hover:text-slate-800 transition duration-150">
                            <i class="fa-solid fa-chevron-right text-xs"></i>
                        </button>
                    </div>
                </div>
                
                <!-- モバイル用一覧表示トグルボタン -->
                <button id="toggleListBtn" class="md:hidden text-slate-600 hover:text-indigo-600 focus:outline-none p-2.5 rounded-xl bg-slate-100">
                    <i class="fa-solid fa-list-check"></i>
                </button>
            </div>

            <!-- カレンダーグリッド -->
            <div class="flex-1 overflow-y-auto p-4 md:p-6">
                <div class="bg-white rounded-2xl shadow-sm border border-slate-200 overflow-hidden">
                    <!-- 曜日ヘッダー -->
                    <div class="grid grid-cols-7 gap-px border-b border-slate-200 bg-slate-50">
                        <div class="py-3 text-center text-xs font-bold text-red-500 uppercase tracking-wider">日</div>
                        <div class="py-3 text-center text-xs font-bold text-slate-600 uppercase tracking-wider">月</div>
                        <div class="py-3 text-center text-xs font-bold text-slate-600 uppercase tracking-wider">火</div>
                        <div class="py-3 text-center text-xs font-bold text-slate-600 uppercase tracking-wider">水</div>
                        <div class="py-3 text-center text-xs font-bold text-slate-600 uppercase tracking-wider">木</div>
                        <div class="py-3 text-center text-xs font-bold text-slate-600 uppercase tracking-wider">金</div>
                        <div class="py-3 text-center text-xs font-bold text-blue-500 uppercase tracking-wider">土</div>
                    </div>
                    
                    <!-- 日付セル -->
                    <div id="calendarGrid" class="grid grid-cols-7 gap-px bg-slate-100 auto-rows-fr" style="min-height: calc(100vh - 200px);">
                        <!-- JavaScriptで動的にカレンダーが生成されます -->
                    </div>
                </div>
            </div>
            
            <!-- モバイル用フローティング予約リスト -->
            <div id="mobileListOverlay" class="absolute inset-0 bg-slate-900/60 z-20 hidden md:hidden flex-col justify-end backdrop-blur-sm">
                <div class="bg-white w-full h-[80%] rounded-t-3xl flex flex-col overflow-hidden shadow-2xl transform transition-transform translate-y-0">
                    <div class="p-4 border-b border-slate-100 flex justify-between items-center">
                        <h2 class="font-bold text-slate-800 text-base flex items-center gap-2">
                            <i class="fa-solid fa-list-check text-indigo-500"></i> 本日の予約一覧
                        </h2>
                        <button id="closeMobileListBtn" class="text-slate-400 hover:text-slate-800 p-2 rounded-full hover:bg-slate-100">
                            <i class="fa-solid fa-times text-lg"></i>
                        </button>
                    </div>
                    <div class="p-3 bg-slate-50 border-b border-slate-100">
                         <input type="text" id="mobileSearchInput" placeholder="お名前やキーワードで検索..." class="w-full px-3.5 py-2 border rounded-xl text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500 bg-white">
                    </div>
                    <div id="mobileReservationList" class="flex-1 overflow-y-auto p-3 space-y-2">
                        <!-- モバイル用リスト -->
                    </div>
                </div>
            </div>

        </section>
    </main>

    <!-- 予約登録/編集モーダル (AI機能付き) -->
    <div id="reservationModal" class="fixed inset-0 z-50 hidden overflow-y-auto" aria-labelledby="modal-title" role="dialog" aria-modal="true">
        <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
            <!-- 背景オーバーレイ -->
            <div class="fixed inset-0 bg-slate-900/40 transition-opacity backdrop-blur-sm" aria-hidden="true" id="modalOverlay"></div>

            <span class="hidden sm:inline-block sm:align-middle sm:h-screen" aria-hidden="true">&#8203;</span>

            <!-- モーダル本体 -->
            <div class="inline-block align-bottom bg-white rounded-2xl text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-xl sm:w-full border border-slate-100">
                
                <!-- タブメニュー (新規作成時のみ表示可能) -->
                <div id="modalTabsHeader" class="bg-slate-50 border-b border-slate-200 flex">
                    <button type="button" id="tabManual" class="flex-1 py-3.5 text-center text-sm font-bold border-b-2 border-indigo-600 text-indigo-600 focus:outline-none flex items-center justify-center gap-2">
                        <i class="fa-solid fa-pen-to-square text-xs"></i> フォームで手動入力
                    </button>
                    <button type="button" id="tabAi" class="flex-1 py-3.5 text-center text-sm font-bold border-b-2 border-transparent text-slate-500 hover:text-slate-800 focus:outline-none flex items-center justify-center gap-2">
                        <i class="fa-solid fa-wand-magic-sparkles text-xs ai-gradient-text"></i> <span class="ai-gradient-text">AIから一括自動入力</span>
                    </button>
                </div>

                <div class="p-5 sm:p-6">
                    <!-- AI自動入力タブの内容 -->
                    <div id="aiTabContent" class="hidden space-y-4">
                        <div class="bg-indigo-50/50 rounded-xl p-3 border border-indigo-100 text-xs text-indigo-700 leading-relaxed flex gap-2">
                            <i class="fa-solid fa-circle-info mt-0.5 text-indigo-500"></i>
                            <div>
                                お客さまからのSNSメッセージ、メール、予約変更などのテキストを下にペーストしてください。AIが自動で内容を抽出し、入力フォームに転記します。
                            </div>
                        </div>

                        <div>
                            <label for="aiInputText" class="block text-xs font-bold text-slate-700 uppercase tracking-wider mb-2">メッセージ内容</label>
                            <textarea id="aiInputText" rows="6" class="w-full border border-slate-200 rounded-xl shadow-sm py-2.5 px-3.5 focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm bg-slate-50" placeholder="【記述例】
来週の金曜（22日）の19時に佐藤ですが、ディナーコースを4名でお願いできますか？
吉田さんの指名で、1名小麦アレルギーがあります。電話番号は 090-9999-9999 です。"></textarea>
                        </div>

                        <div class="flex justify-end">
                            <button type="button" id="runAiExtractBtn" class="ai-gradient-bg hover:opacity-95 text-white font-bold py-2.5 px-5 rounded-xl shadow-md flex items-center text-sm gap-2 transition duration-150">
                                <i class="fa-solid fa-sparkles"></i> <span>AIで解析してフォームを埋める</span>
                            </button>
                        </div>
                    </div>

                    <!-- 手動フォームの内容（AIパースされたものもここに入ります） -->
                    <form id="reservationForm" class="space-y-4">
                        <input type="hidden" id="formMode" value="create"> <!-- create or edit -->
                        <input type="hidden" id="reservationId" value="">

                        <h3 class="text-base font-bold text-slate-800 pb-2 border-b border-slate-100" id="modalTitle">
                            新規予約の登録
                        </h3>

                        <!-- 顧客名 -->
                        <div>
                            <label for="customerName" class="block text-xs font-bold text-slate-700 uppercase tracking-wider mb-1.5">お名前 <span class="text-rose-500">*</span></label>
                            <input type="text" name="customerName" id="customerName" required class="block w-full border border-slate-200 rounded-xl shadow-sm py-2 px-3 focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm" placeholder="山田 太郎">
                        </div>

                        <!-- 連絡先 -->
                        <div>
                            <label for="contactInfo" class="block text-xs font-bold text-slate-700 uppercase tracking-wider mb-1.5">電話番号</label>
                            <input type="tel" name="contactInfo" id="contactInfo" class="block w-full border border-slate-200 rounded-xl shadow-sm py-2 px-3 focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm" placeholder="090-1234-5678">
                        </div>

                        <div class="grid grid-cols-2 gap-4">
                            <!-- 日付 -->
                            <div>
                                <label for="resDate" class="block text-xs font-bold text-slate-700 uppercase tracking-wider mb-1.5">日付 <span class="text-rose-500">*</span></label>
                                <input type="date" name="resDate" id="resDate" required class="block w-full border border-slate-200 rounded-xl shadow-sm py-2 px-3 focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm">
                            </div>
                            
                            <!-- 時間 -->
                            <div>
                                <label for="resTime" class="block text-xs font-bold text-slate-700 uppercase tracking-wider mb-1.5">時間 <span class="text-rose-500">*</span></label>
                                <select name="resTime" id="resTime" required class="block w-full border border-slate-200 rounded-xl shadow-sm py-2 px-3 focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm">
                                    <!-- JavaScriptで時間を生成 -->
                                </select>
                            </div>
                        </div>

                        <!-- メニューと担当 -->
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label for="menu" class="block text-xs font-bold text-slate-700 uppercase tracking-wider mb-1.5">メニュー/コース</label>
                                <select name="menu" id="menu" class="block w-full border border-slate-200 rounded-xl shadow-sm py-2 px-3 focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm bg-white">
                                    <option value="">指定なし</option>
                                    <option value="ランチコース">ランチコース</option>
                                    <option value="ディナーコース">ディナーコース</option>
                                    <option value="カット">カット</option>
                                    <option value="カット＆カラー">カット＆カラー</option>
                                    <option value="ネイルケア">ネイルケア</option>
                                </select>
                            </div>
                            <div>
                                <label for="staff" class="block text-xs font-bold text-slate-700 uppercase tracking-wider mb-1.5">担当スタッフ</label>
                                <select name="staff" id="staff" class="block w-full border border-slate-200 rounded-xl shadow-sm py-2 px-3 focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm bg-white">
                                    <option value="">指名なし</option>
                                    <option value="田中">田中</option>
                                    <option value="佐藤">佐藤</option>
                                    <option value="吉田">吉田</option>
                                </select>
                            </div>
                        </div>

                        <!-- 人数・ステータス -->
                        <div class="grid grid-cols-2 gap-4">
                            <div>
                                <label for="partySize" class="block text-xs font-bold text-slate-700 uppercase tracking-wider mb-1.5">人数</label>
                                <input type="number" min="1" max="20" name="partySize" id="partySize" value="1" class="block w-full border border-slate-200 rounded-xl shadow-sm py-2 px-3 focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm">
                            </div>
                            <div>
                                <label for="status" class="block text-xs font-bold text-slate-700 uppercase tracking-wider mb-1.5">ステータス</label>
                                <select name="status" id="status" class="block w-full border border-slate-200 rounded-xl shadow-sm py-2 px-3 focus:outline-none focus:ring-2 focus:ring-indigo-500 text-sm bg-white">
                                    <option value="confirmed" selected>確定</option>
                                    <option value="pending">仮予約</option>
                                    <option value="cancelled">キャンセル</option>
                                </select>
                            </div>
                        </div>

                        <!-- メモ -->
                        <div>
                            <label for="notes" class="block text-xs font-bold text-slate-700 uppercase tracking-wider mb-1.5">メモ・ご要望</label>
                            <textarea id="notes" name="notes" rows="2" class="block w-full border border-slate-200 rounded-xl shadow-sm focus:ring-2 focus:ring-indigo-500 text-sm py-2 px-3" placeholder="アレルギーや特記事項など..."></textarea>
                        </div>

                        <!-- 【AI返信作成セクション - 編集時のみ表示】 -->
                        <div id="aiReplySection" class="hidden border-t border-slate-200 pt-4 mt-4 bg-purple-50/50 p-4 rounded-xl border border-purple-100">
                            <h4 class="text-xs font-bold text-purple-900 flex items-center gap-1.5 mb-2.5">
                                <i class="fa-solid fa-wand-magic-sparkles ai-gradient-text"></i> AIメッセージ返信アシスタント
                            </h4>
                            <div class="grid grid-cols-2 gap-3 mb-3">
                                <div>
                                    <label for="aiReplyTone" class="block text-[10px] font-bold text-purple-700 mb-1">トーン・状況</label>
                                    <select id="aiReplyTone" class="block w-full border border-purple-200 rounded-lg shadow-sm py-1.5 px-2.5 text-xs focus:ring-indigo-500 bg-white">
                                        <option value="confirm_normal">ご予約確定（標準）</option>
                                        <option value="confirm_polite">ご予約確定（丁寧）</option>
                                        <option value="pending_notice">仮予約のお知らせ</option>
                                        <option value="cancellation_apology">キャンセル確認・お詫び</option>
                                        <option value="reminder">前日リマインダー</option>
                                    </select>
                                </div>
                                <div>
                                    <label for="aiReplyChannel" class="block text-[10px] font-bold text-purple-700 mb-1">配信ツール</label>
                                    <select id="aiReplyChannel" class="block w-full border border-purple-200 rounded-lg shadow-sm py-1.5 px-2.5 text-xs focus:ring-indigo-500 bg-white">
                                        <option value="sns">LINE / SMS（短め）</option>
                                        <option value="email">Eメール（フォーマル）</option>
                                    </select>
                                </div>
                            </div>
                            <button type="button" id="generateAiReplyBtn" class="w-full bg-purple-600 hover:bg-purple-700 text-white font-bold py-2 px-3 rounded-lg shadow-sm flex items-center justify-center text-xs gap-1.5 transition">
                                <i class="fa-solid fa-magic animate-pulse"></i> <span>返信テンプレート文面を生成</span>
                            </button>

                            <!-- 生成された文面の表示エリア -->
                            <div id="aiReplyOutputContainer" class="hidden mt-3 space-y-2">
                                <textarea id="aiReplyOutput" rows="4" class="w-full border border-purple-200 rounded-lg py-2 px-3 text-xs bg-white text-slate-800 focus:outline-none focus:ring-2 focus:ring-purple-500 leading-relaxed"></textarea>
                                <div class="flex justify-end gap-2">
                                    <button type="button" id="copyAiReplyBtn" class="bg-white hover:bg-slate-50 text-slate-700 border border-slate-200 text-xs font-semibold py-1.5 px-3 rounded-lg flex items-center gap-1.5 transition">
                                        <i class="fa-regular fa-copy"></i> コピーする
                                    </button>
                                </div>
                            </div>
                        </div>

                        <!-- フッターボタン -->
                        <div class="bg-slate-50 -mx-5 -mb-5 sm:-mx-6 sm:-mb-6 px-6 py-4 flex flex-row-reverse justify-between border-t border-slate-100 gap-2">
                            <div class="flex gap-2">
                                <button type="submit" class="inline-flex justify-center rounded-xl shadow-sm px-4.5 py-2.5 bg-indigo-600 text-sm font-bold text-white hover:bg-indigo-700 focus:outline-none transition">
                                    保存する
                                </button>
                                <button type="button" id="cancelModalBtn" class="inline-flex justify-center rounded-xl border border-slate-200 shadow-sm px-4.5 py-2.5 bg-white text-sm font-bold text-slate-700 hover:bg-slate-50 focus:outline-none transition">
                                    キャンセル
                                </button>
                            </div>
                            
                            <!-- 編集時のみ表示する削除ボタン -->
                            <button type="button" id="deleteReservationBtn" class="hidden inline-flex justify-center rounded-xl border border-rose-200 shadow-sm px-4.5 py-2.5 bg-rose-50 text-sm font-bold text-rose-600 hover:bg-rose-100 focus:outline-none transition">
                                <i class="fa-solid fa-trash-can mr-1.5 mt-0.5"></i> 削除
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>

    <!-- AI予約分析モーダル (AI Advisor) -->
    <div id="aiAdvisorModal" class="fixed inset-0 z-50 hidden overflow-y-auto" aria-labelledby="modal-title" role="dialog" aria-modal="true">
        <div class="flex items-center justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
            <div class="fixed inset-0 bg-slate-900/40 transition-opacity backdrop-blur-sm" aria-hidden="true" id="aiAdvisorOverlay"></div>
            <span class="hidden sm:inline-block sm:align-middle sm:h-screen" aria-hidden="true">&#8203;</span>

            <div class="inline-block align-middle bg-white rounded-2xl text-left overflow-hidden shadow-2xl transform transition-all sm:my-8 sm:align-middle sm:max-w-xl sm:w-full border border-slate-100">
                <div class="bg-gradient-to-tr from-indigo-900 to-purple-900 text-white p-6 relative">
                    <div class="absolute right-4 top-4">
                        <button id="closeAiAdvisorBtn" class="text-white/80 hover:text-white p-2 rounded-full hover:bg-white/10">
                            <i class="fa-solid fa-times text-lg"></i>
                        </button>
                    </div>
                    <div class="flex items-center gap-3">
                        <div class="bg-white/10 rounded-xl p-3 flex items-center justify-center">
                            <i class="fa-solid fa-brain text-2xl text-indigo-300"></i>
                        </div>
                        <div>
                            <h3 class="text-lg font-bold">AI予約アドバイザー分析</h3>
                            <p class="text-xs text-indigo-200">今日の予約データのトレンド・業務予測アドバイス</p>
                        </div>
                    </div>
                </div>

    <!-- 【新規追加】データ管理モーダル（PC保存・復元） -->
    <div id="dataManagementModal" class="fixed inset-0 z-50 hidden overflow-y-auto" aria-labelledby="modal-title" role="dialog" aria-modal="true">
        <div class="flex items-center justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
            <div class="fixed inset-0 bg-slate-900/40 transition-opacity backdrop-blur-sm" aria-hidden="true" id="dataManagementOverlay"></div>
            <span class="hidden sm:inline-block sm:align-middle sm:h-screen" aria-hidden="true">&#8203;</span>

            <div class="inline-block align-middle bg-white rounded-2xl text-left overflow-hidden shadow-2xl transform transition-all sm:my-8 sm:align-middle sm:max-w-md sm:w-full border border-slate-100">
                <div class="p-6">
                    <h3 class="text-lg font-bold text-slate-900 mb-4 flex items-center gap-2">
                        <i class="fa-solid fa-database text-indigo-600"></i>
                        <span>予約データのバックアップ・復元</span>
                    </h3>
                    <p class="text-xs text-slate-500 mb-5 leading-relaxed">
                        予約データはパソコンのブラウザ（LocalStorage）に自動保存されますが、ブラウザのキャッシュ削除などで消えるのを防ぐため、ファイルとしてPC内に保存しておくことができます。
                    </p>

                    <div class="space-y-4">
                        <!-- エクスポート -->
                        <div class="p-4 bg-slate-50 rounded-xl border border-slate-200">
                            <h4 class="text-sm font-bold text-slate-800 mb-1 flex items-center gap-1.5">
                                <i class="fa-solid fa-file-arrow-down text-emerald-600"></i> パソコンへデータを保存する
                            </h4>
                            <p class="text-[11px] text-slate-500 mb-3">
                                現在登録されているすべての予約データをJSONファイルとしてダウンロードします。
                            </p>
                            <button id="exportBtn" class="w-full bg-emerald-600 hover:bg-emerald-700 text-white text-xs font-bold py-2 px-3 rounded-lg flex items-center justify-center gap-1.5 transition">
                                <i class="fa-solid fa-download"></i> <span>バックアップファイルをダウンロード</span>
                            </button>
                        </div>

                        <!-- インポート -->
                        <div class="p-4 bg-slate-50 rounded-xl border border-slate-200">
                            <h4 class="text-sm font-bold text-slate-800 mb-1 flex items-center gap-1.5">
                                <i class="fa-solid fa-file-arrow-up text-indigo-600"></i> パソコンからデータを読み込む
                            </h4>
                            <p class="text-[11px] text-slate-500 mb-3">
                                以前ダウンロードしたバックアップファイルを読み込んでデータを復元します。<br>
                                <span class="text-rose-500 font-semibold">※現在のデータは上書きされます。</span>
                            </p>
                            <label class="w-full bg-white hover:bg-slate-50 text-slate-700 border border-slate-300 border-dashed text-xs font-bold py-2 px-3 rounded-lg flex items-center justify-center gap-1.5 transition cursor-pointer">
                                <i class="fa-solid fa-upload"></i> <span>ファイルを選択して復元</span>
                                <input type="file" id="importFile" class="hidden" accept=".json">
                            </label>
                        </div>
                    </div>
                </div>

                <div class="bg-slate-100 px-6 py-4 flex justify-end border-t border-slate-200">
                    <button type="button" id="closeDataModalBtn" class="rounded-xl px-4 py-2 bg-slate-900 text-xs font-bold text-white hover:bg-slate-800 transition">
                        閉じる
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- トースト通知 -->
    <div id="toastContainer" class="fixed bottom-5 right-5 z-50 flex flex-col gap-2"></div>

    <script>
        // --- 状態管理と初期データ ---
        // 初回ロード時は、PC内のブラウザに保存されたデータ（LocalStorage）を読み込みます。
        // 保存データがない場合は、デモ用の初期データをロードします。
        const defaultReservations = [
            { id: "res-1", customerName: "佐藤 花子", contactInfo: "090-1111-2222", date: "2026-05-18", time: "10:00", partySize: 2, status: "confirmed", notes: "窓側の席希望、お誕生日ケーキ持ち込み", menu: "ランチコース", staff: "田中" },
            { id: "res-2", customerName: "鈴木 一郎", contactInfo: "080-3333-4444", date: "2026-05-18", time: "13:30", partySize: 1, status: "confirmed", notes: "小麦アレルギーあり", menu: "カット", staff: "吉田" },
            { id: "res-3", customerName: "高橋 健太", contactInfo: "070-5555-6666", date: "2026-05-20", time: "18:00", partySize: 4, status: "pending", notes: "バースデープレート希望", menu: "ディナーコース", staff: "" },
            { id: "res-4", customerName: "伊藤 結衣", contactInfo: "", date: "2026-05-25", time: "11:00", partySize: 2, status: "cancelled", notes: "体調不良のため", menu: "ネイルケア", staff: "" }
        ];

        let reservations = [];
        
        // データの読み込み
        function loadReservationsFromStorage() {
            const stored = localStorage.getItem('reservations_data');
            if (stored) {
                try {
                    reservations = JSON.parse(stored);
                } catch (e) {
                    console.error("データの破損を検知したためデフォルトデータを使用します", e);
                    reservations = [...defaultReservations];
                }
            } else {
                reservations = [...defaultReservations];
                saveReservationsToStorage();
            }
        }

        // データの書き込み
        function saveReservationsToStorage() {
            localStorage.setItem('reservations_data', JSON.stringify(reservations));
        }

        let currentDate = new Date(2026, 4, 18); // 2026年5月18日を基準
        const today = new Date(2026, 4, 18);

        // API KeyはCanvas環境で自動提供。手動で他モデル利用時はここに入力
        const apiKey = ""; 

        // --- UI要素取得 ---
        const calendarGrid = document.getElementById('calendarGrid');
        const currentMonthYearDisplay = document.getElementById('currentMonthYear');
        const prevMonthBtn = document.getElementById('prevMonthBtn');
        const nextMonthBtn = document.getElementById('nextMonthBtn');
        const todayBtn = document.getElementById('todayBtn');
        
        const reservationList = document.getElementById('reservationList');
        const mobileReservationList = document.getElementById('mobileReservationList');
        const todayDateDisplay = document.getElementById('todayDate');
        const searchInput = document.getElementById('searchInput');
        const mobileSearchInput = document.getElementById('mobileSearchInput');
        
        const modal = document.getElementById('reservationModal');
        const openModalBtn = document.getElementById('openModalBtn');
        const cancelModalBtn = document.getElementById('cancelModalBtn');
        const modalOverlay = document.getElementById('modalOverlay');
        const reservationForm = document.getElementById('reservationForm');
        const deleteReservationBtn = document.getElementById('deleteReservationBtn');
        
        const toggleListBtn = document.getElementById('toggleListBtn');
        const mobileListOverlay = document.getElementById('mobileListOverlay');
        const closeMobileListBtn = document.getElementById('closeMobileListBtn');

        // データ管理関連のUI要素
        const dataManagementBtn = document.getElementById('dataManagementBtn');
        const dataManagementModal = document.getElementById('dataManagementModal');
        const dataManagementOverlay = document.getElementById('dataManagementOverlay');
        const closeDataModalBtn = document.getElementById('closeDataModalBtn');
        const exportBtn = document.getElementById('exportBtn');
        const importFile = document.getElementById('importFile');

        // AI関連要素
        const tabManual = document.getElementById('tabManual');
        const tabAi = document.getElementById('tabAi');
        const aiTabContent = document.getElementById('aiTabContent');
        const modalTabsHeader = document.getElementById('modalTabsHeader');
        
        const runAiExtractBtn = document.getElementById('runAiExtractBtn');
        const aiInputText = document.getElementById('aiInputText');
        
        const aiReplySection = document.getElementById('aiReplySection');
        const generateAiReplyBtn = document.getElementById('generateAiReplyBtn');
        const aiReplyTone = document.getElementById('aiReplyTone');
        const aiReplyChannel = document.getElementById('aiReplyChannel');
        const aiReplyOutputContainer = document.getElementById('aiReplyOutputContainer');
        const aiReplyOutput = document.getElementById('aiReplyOutput');
        const copyAiReplyBtn = document.getElementById('copyAiReplyBtn');

        const aiAdvisorBtn = document.getElementById('aiAdvisorBtn');
        const aiAdvisorModal = document.getElementById('aiAdvisorModal');
        const aiAdvisorOverlay = document.getElementById('aiAdvisorOverlay');
        const closeAiAdvisorBtn = document.getElementById('closeAiAdvisorBtn');
        const closeAiAdvisorBtn2 = document.getElementById('closeAiAdvisorBtn2');
        const aiAdvisorLoading = document.getElementById('aiAdvisorLoading');
        const aiAdvisorResult = document.getElementById('aiAdvisorResult');
        const aiAdvisorOutput = document.getElementById('aiAdvisorOutput');
        const aiSummaryText = document.getElementById('aiSummaryText');

        // --- 初期起動 ---
        function init() {
            loadReservationsFromStorage(); // PC内の保存データを読み込み
            generateTimeOptions();
            const options = { year: 'numeric', month: 'long', day: 'numeric', weekday: 'short' };
            todayDateDisplay.textContent = today.toLocaleDateString('ja-JP', options);
            
            renderCalendar(currentDate);
            renderReservationList();
            setupEventListeners();
            
            // 起動時に軽く本日のサマリーのプレビューを裏で読み込んでおく
            preloadSummary();
        }

        // --- ヘルパー関数 ---
        function formatDateString(date) {
            const year = date.getFullYear();
            const month = String(date.getMonth() + 1).padStart(2, '0');
            const day = String(date.getDate()).padStart(2, '0');
            return `${year}-${month}-${day}`;
        }

        function generateTimeOptions() {
            const select = document.getElementById('resTime');
            select.innerHTML = '';
            for (let hour = 9; hour <= 21; hour++) {
                for (let min of ['00', '30']) {
                    if (hour === 21 && min === '30') continue;
                    const timeString = `${String(hour).padStart(2, '0')}:${min}`;
                    const option = document.createElement('option');
                    option.value = timeString;
                    option.textContent = timeString;
                    select.appendChild(option);
                }
            }
        }

        function showToast(message, type = 'success') {
            const container = document.getElementById('toastContainer');
            const toast = document.createElement('div');
            
            let bgClass = type === 'success' ? 'bg-emerald-600 shadow-emerald-100' : (type === 'error' ? 'bg-rose-600 shadow-rose-100' : 'bg-slate-800 shadow-slate-100');
            toast.className = `${bgClass} text-white px-4 py-3 rounded-xl shadow-lg flex items-center gap-3 transform transition-all duration-300 translate-y-10 opacity-0 text-sm font-semibold border border-white/10`;
            
            const icon = type === 'success' ? 'fa-check-circle' : (type === 'error' ? 'fa-exclamation-circle' : 'fa-info-circle');
            toast.innerHTML = `<i class="fa-solid ${icon}"></i> <span>${message}</span>`;
            
            container.appendChild(toast);
            setTimeout(() => toast.classList.remove('translate-y-10', 'opacity-0'), 10);
            setTimeout(() => {
                toast.classList.add('translate-y-10', 'opacity-0');
                setTimeout(() => toast.remove(), 300);
            }, 4000);
        }

        function getStatusBadgeClass(status) {
            switch(status) {
                case 'confirmed': return 'bg-emerald-50 text-emerald-700 border-emerald-200';
                case 'pending': return 'bg-amber-50 text-amber-700 border-amber-200';
                case 'cancelled': return 'bg-rose-50 text-rose-700 border-rose-200';
                default: return 'bg-slate-50 text-slate-700 border-slate-200';
            }
        }
        function getStatusText(status) {
             switch(status) {
                case 'confirmed': return '確定';
                case 'pending': return '仮予約';
                case 'cancelled': return 'キャンセル';
                default: return status;
            }
        }

        // --- STREAMING_CHUNK: Integrating Gemini LLM API fetch logic... ---
        // Gemini API 呼び出し用の共通関数
        async function fetchGemini(userPrompt, systemPrompt = "", responseSchema = null) {
            const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${apiKey}`;
            
            const payload = {
                contents: [{ parts: [{ text: userPrompt }] }]
            };

            if (systemPrompt) {
                payload.systemInstruction = {
                    parts: [{ text: systemPrompt }]
                };
            }

            if (responseSchema) {
                payload.generationConfig = {
                    responseMimeType: "application/json",
                    responseSchema: responseSchema
                };
            }

            // 指数バックオフ付きのリトライ処理
            let delay = 1000;
            for (let attempt = 0; attempt < 3; attempt++) {
                try {
                    const response = await fetch(apiUrl, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });

                    if (!response.ok) {
                        throw new Error(`HTTP Error! status: ${response.status}`);
                    }

                    const result = await response.json();
                    const candidate = result.candidates?.[0];
                    if (candidate && candidate.content?.parts?.[0]?.text) {
                        return candidate.content.parts[0].text;
                    } else {
                        throw new Error("Invalid response format from Gemini");
                    }
                } catch (error) {
                    if (attempt === 2) throw error;
                    await new Promise(resolve => setTimeout(resolve, delay));
                    delay *= 2;
                }
            }
        }

        // --- STREAMING_CHUNK: AI Feature 1: Intelligent Auto-fill Form... ---
        // AI自然言語テキスト解析（一括入力）
        async function runAiExtraction() {
            const text = aiInputText.value.trim();
            if (!text) {
                showToast("メッセージが空です。解析したい内容を入力してください。", "error");
                return;
            }

            // 解析中のアニメーション
            runAiExtractBtn.disabled = true;
            runAiExtractBtn.innerHTML = `<i class="fa-solid fa-spinner animate-spin"></i> <span>解析中...</span>`;

            // 今日の日付をベースに相対的な日付を割り出しやすくする
            const systemPrompt = `あなたは飲食店およびサロン用の高精度な予約解析コパイロットです。
ユーザーから入力されたメッセージ（SNSやメールの断片など）を分析し、JSONデータとして正確に出力してください。

【制約・解釈ルール】
- 基準日（本日）は「2026-05-18 (月曜日)」です。
- 「明日」なら 2026-05-19、「来週金曜」なら 2026-05-29 など、基準日からカレンダー上の実際の日付(YYYY-MM-DD形式)を絶対に正しく計算してください。
- メニュー(menu)は、次のいずれかにぴったり合う、または最も近いものに変換してください。一致しない場合は空文字にしてください: ['ランチコース', 'ディナーコース', 'カット', 'カット＆カラー', 'ネイルケア']
- スタッフ(staff)は、次のいずれかにぴったり合う、または最も近いものに変換してください。一致しない場合は空文字にしてください: ['田中', '佐藤', '吉田']
- 時間(time)は「18:00」「13:30」のような 24時間表記 HH:MM 形式の30分刻みに最適化してください。`;

            const schema = {
                type: "OBJECT",
                properties: {
                    customerName: { type: "STRING" },
                    contactInfo: { type: "STRING" },
                    date: { type: "STRING", description: "YYYY-MM-DD形式の日付" },
                    time: { type: "STRING", description: "HH:MM形式の時間(9:00〜21:00、30分刻みの最適なもの)" },
                    partySize: { type: "INTEGER" },
                    menu: { type: "STRING" },
                    staff: { type: "STRING" },
                    notes: { type: "STRING", description: "アレルギー、要望、指名などの詳細情報" }
                },
                required: ["customerName", "date", "time"]
            };

            try {
                const jsonText = await fetchGemini(text, systemPrompt, schema);
                const parsed = JSON.parse(jsonText);

                // 各フォームに反映
                if (parsed.customerName) document.getElementById('customerName').value = parsed.customerName;
                if (parsed.contactInfo) document.getElementById('contactInfo').value = parsed.contactInfo;
                if (parsed.date) document.getElementById('resDate').value = parsed.date;
                if (parsed.time) document.getElementById('resTime').value = parsed.time;
                if (parsed.partySize) document.getElementById('partySize').value = parsed.partySize;
                if (parsed.menu) document.getElementById('menu').value = parsed.menu;
                if (parsed.staff) document.getElementById('staff').value = parsed.staff;
                if (parsed.notes) document.getElementById('notes').value = parsed.notes;

                showToast("AIが予約内容を分析し、フォームに転記しました！", "success");
                
                // タブを手動入力（フォームビュー）に戻す
                switchTab('manual');
            } catch (error) {
                console.error("AI解析エラー:", error);
                showToast("AI解析に失敗しました。時間やフォーマット等を手動でご確認ください。", "error");
            } finally {
                runAiExtractBtn.disabled = false;
                runAiExtractBtn.innerHTML = `<i class="fa-solid fa-sparkles"></i> <span>AIで解析してフォームを埋める</span>`;
            }
        }

        // --- STREAMING_CHUNK: AI Feature 2: Response Draft Generator... ---
        // AIメッセージ返信文面生成
        async function runAiReplyGeneration() {
            const tone = aiReplyTone.value;
            const channel = aiReplyChannel.value;

            // 現在のフォームの値をリアルタイムに集計してインプットとする
            const resData = {
                customerName: document.getElementById('customerName').value,
                date: document.getElementById('resDate').value,
                time: document.getElementById('resTime').value,
                partySize: document.getElementById('partySize').value,
                menu: document.getElementById('menu').value || "指定なし",
                staff: document.getElementById('staff').value || "指名なし",
                notes: document.getElementById('notes').value
            };

            if (!resData.customerName || !resData.date || !resData.time) {
                showToast("お名前、日付、時間を入力した状態で作成してください。", "error");
                return;
            }

            generateAiReplyBtn.disabled = true;
            generateAiReplyBtn.innerHTML = `<i class="fa-solid fa-spinner animate-spin"></i> <span>返信案を作成中...</span>`;
            aiReplyOutputContainer.classList.add('hidden');

            const prompt = `以下の予約情報をベースに、お客さまへの返信文面をプロフェッショナルかつ温かみをもって作成してください。

【予約情報】
- 顧客名: ${resData.customerName} 様
- 日時: ${resData.date} ${resData.time}〜
- 人数: ${resData.partySize}名
- メニュー/コース: ${resData.menu}
- 担当スタッフ: ${resData.staff}
- 特記事項/ご要望: ${resData.notes || "特になし"}

【作成オプション】
- トーン種類: ${tone} (「confirm_normal: 予約確定案内(標準)」「confirm_polite: 予約確定(丁寧)」「pending_notice: 空き枠再提示を伴う仮予約状況通知」「cancellation_apology: キャンセル確認と次回お勧めのお詫び」「reminder: 前日リマインダー」)
- 送信ツール種類: ${channel} (「sns: LINEやSMSなどの短文・フレンドリー」「email: 通常の丁寧なビジネスメール」)

不要な前置きや「承知いたしました」といった二重応答は省き、そのままお客様に送信できる完成されたテンプレートメッセージを出力してください。挨拶や文末に署名枠 [店舗名] 等を入れてください。`;

            try {
                const generatedText = await fetchGemini(prompt, "あなたはホスピタリティあふれる飲食店・サロンの店長です。");
                aiReplyOutput.value = generatedText;
                aiReplyOutputContainer.classList.remove('hidden');
                showToast("AIが最適な返信文面を生成しました！", "success");
            } catch (error) {
                console.error("AIメッセージ作成エラー:", error);
                showToast("文面の生成に失敗しました。再度お試しください。", "error");
            } finally {
                generateAiReplyBtn.disabled = false;
                generateAiReplyBtn.innerHTML = `<i class="fa-solid fa-magic"></i> <span>返信テンプレート文面を生成</span>`;
            }
        }

        // --- STREAMING_CHUNK: AI Feature 3: Live Summary & Daily Advisor... ---
        // 簡易プレロードサマリー (サイドバーに表示するもの)
        async function preloadSummary() {
            const todayStr = formatDateString(today);
            const todayRes = reservations.filter(r => r.date === todayStr && r.status !== 'cancelled');
            
            if (todayRes.length === 0) {
                aiSummaryText.textContent = "本日の予約はありません。ゆったりしたシフト編成や、集客マーケティングの検討日として最適です。";
                return;
            }

            const dataBrief = todayRes.map(r => `${r.time} ${r.customerName}(${r.partySize}名) ${r.menu} 担当:${r.staff} メモ:${r.notes}`).join('\n');
            const prompt = `以下の本日の予約データ（2026-05-18）の概略を元に、店長・店舗スタッフにむけた、本日の簡単な一言ブリーフィング要約（100文字程度）を1文で書いてください。混雑度や、アレルギー等の要注意ポイントについて触れてください。
            
【本日の予約】
${dataBrief}`;

            try {
                const summary = await fetchGemini(prompt, "あなたは店舗運営を支えるインテリジェントな分析アシスタントです。非常に簡潔に、要点のみをアドバイスしてください。");
                aiSummaryText.textContent = summary;
            } catch (error) {
                console.warn("サマリー事前ロードエラー:", error);
            }
        }

        // AI予約アドバイザー分析（詳細レポート）
        async function triggerDailySummary() {
            aiAdvisorModal.classList.remove('hidden');
            aiAdvisorLoading.classList.remove('hidden');
            aiAdvisorResult.classList.add('hidden');

            const todayStr = formatDateString(today);
            // キャンセルされた予約も含めて全体を客観的に見せる
            const todayRes = reservations.filter(r => r.date === todayStr);

            if (todayRes.length === 0) {
                aiAdvisorOutput.innerHTML = `
                    <div class="text-center py-6">
                        <i class="fa-regular fa-calendar text-4xl text-slate-300 mb-3"></i>
                        <p class="font-bold text-slate-700">本日の予約データがありません</p>
                        <p class="text-xs text-slate-500 mt-1">予約がない日は、SNSやWEBのマーケティング施策、店舗の清掃やスタッフミーティングを計画することをお勧めします。</p>
                    </div>`;
                aiAdvisorLoading.classList.add('hidden');
                aiAdvisorResult.classList.remove('hidden');
                return;
            }

            const todayReservationsText = todayRes.map(r => {
                return `- 【時間】${r.time} 【名前】${r.customerName} 【人数】${r.partySize}名 【ステータス】${getStatusText(r.status)} 【メニュー】${r.menu || 'なし'} 【担当】${r.staff || 'フリー'} 【要望】${r.notes || 'なし'}`;
            }).join('\n');

            const prompt = `今日は 2026年5月18日（月曜日）です。
以下の本日の予約リストを元に、本日の店舗オペレーションへの具体的な業務アドバイスや、混雑度の傾向、お客様からの特別なリクエスト・アレルギー対応における重要ポイントなどを分析・提示してください。

【本日の予約リスト】
${todayReservationsText}

【出力内容の構成（HTMLのタグを使用して見栄え良く見出し・重要ポイントなどを分けて構成してください）】
1. **本日の店舗混雑傾向とアドバイス** (時間帯別のピーク、業務の優先順位など)
2. **要注意・特別対応が必要なお客さま** (アレルギーや記念日などのピックアップ)
3. **スタッフ配置・役割のアドバイス** (田中の稼働が多い、吉田にゆとりがある、など担当状況の提案)
4. **本日のワンポイント売上アップ/集客提案** (当日空き時間をどうアピールするかなど)`;

            try {
                const mdResult = await fetchGemini(prompt, "あなたは店舗コンサルタントのAIアドバイザーです。飲食店やサロンに的確でホスピタリティに満ちた現実的なアドバイスをします。");
                
                // マークダウン風の強調表現等をHTMLにパースして埋め込む（※Geminiから返ってくる **強** などを簡単な置換でリストやカードにする）
                let formattedHtml = mdResult
                    .replace(/\*\*(.*?)\*\*/g, '<strong class="text-slate-900 font-bold">$1</strong>')
                    .replace(/### (.*?)\n/g, '<h4 class="text-sm font-bold text-indigo-900 mt-4 mb-1.5 flex items-center gap-1.5"><i class="fa-solid fa-angle-right text-indigo-500"></i> $1</h4>')
                    .replace(/## (.*?)\n/g, '<h3 class="text-base font-bold text-indigo-900 border-b pb-1 mt-5 mb-2 flex items-center gap-2"><i class="fa-solid fa-star ai-gradient-text"></i> $1</h3>')
                    .replace(/^- (.*?)\n/gm, '<li class="ml-4 list-disc text-slate-600">$1</li>')
                    .replace(/\n\n/g, '<p class="mb-2 leading-relaxed"></p>');

                aiAdvisorOutput.innerHTML = formattedHtml;
                aiAdvisorLoading.classList.add('hidden');
                aiAdvisorResult.classList.remove('hidden');
            } catch (error) {
                console.error("AIアドバイザーエラー:", error);
                aiAdvisorOutput.innerHTML = `<div class="text-rose-600 text-center"><i class="fa-solid fa-triangle-exclamation text-2xl mb-2"></i><p>AIアドバイスの作成中にエラーが発生しました。時間を置いて再度お試しください。</p></div>`;
                aiAdvisorLoading.classList.add('hidden');
                aiAdvisorResult.classList.remove('hidden');
            }
        }

        // --- STREAMING_CHUNK: Managing Modal Form tabs and layouts... ---
        // タブ切り替え制御
        function switchTab(tab) {
            if (tab === 'manual') {
                tabManual.classList.add('border-indigo-600', 'text-indigo-600');
                tabManual.classList.remove('border-transparent', 'text-slate-500');
                tabAi.classList.add('border-transparent', 'text-slate-500');
                tabAi.classList.remove('border-indigo-600', 'text-indigo-600');
                
                reservationForm.classList.remove('hidden');
                aiTabContent.classList.add('hidden');
            } else {
                tabAi.classList.add('border-indigo-600', 'text-indigo-600');
                tabAi.classList.remove('border-transparent', 'text-slate-500');
                tabManual.classList.add('border-transparent', 'text-slate-500');
                tabManual.classList.remove('border-indigo-600', 'text-indigo-600');
                
                reservationForm.classList.add('hidden');
                aiTabContent.classList.remove('hidden');
            }
        }

        // --- カレンダー描画 ---
        function renderCalendar(date) {
            const year = date.getFullYear();
            const month = date.getMonth();
            
            currentMonthYearDisplay.textContent = `${year}年 ${month + 1}月`;
            
            const firstDay = new Date(year, month, 1);
            const lastDay = new Date(year, month + 1, 0);
            const startingDayIndex = firstDay.getDay();
            
            calendarGrid.innerHTML = '';
            
            // 前月の日付
            const prevMonthLastDay = new Date(year, month, 0).getDate();
            for (let i = 0; i < startingDayIndex; i++) {
                const dayNum = prevMonthLastDay - startingDayIndex + i + 1;
                calendarGrid.appendChild(createCalendarCell(year, month - 1, dayNum, true));
            }
            
            // 当月の日付
            const todayStr = formatDateString(today);
            for (let i = 1; i <= lastDay.getDate(); i++) {
                const cellDateStr = formatDateString(new Date(year, month, i));
                const isToday = cellDateStr === todayStr;
                calendarGrid.appendChild(createCalendarCell(year, month, i, false, isToday));
            }
            
            // 翌月の日付
            const totalCells = startingDayIndex + lastDay.getDate();
            const remainingCells = 42 - totalCells;
            for (let i = 1; i <= remainingCells; i++) {
                calendarGrid.appendChild(createCalendarCell(year, month + 1, i, true));
            }
        }

        function createCalendarCell(year, month, day, isOtherMonth, isToday = false) {
            const cellDate = new Date(year, month, day);
            const dateString = formatDateString(cellDate);
            
            const cell = document.createElement('div');
            cell.className = `bg-white min-h-[110px] p-2 flex flex-col transition-all border-b border-r border-slate-100 ${isOtherMonth ? 'bg-slate-50/50' : 'hover:bg-indigo-50/50 cursor-pointer'}`;
            
            if(!isOtherMonth) {
                cell.onclick = () => {
                    openModal('create');
                    document.getElementById('resDate').value = dateString;
                };
            }

            const headerDiv = document.createElement('div');
            headerDiv.className = 'flex justify-between items-start';
            
            const daySpan = document.createElement('span');
            daySpan.textContent = day;
            let dayClass = 'text-xs font-bold w-6 h-6 flex items-center justify-center rounded-lg ';
            
            if (isOtherMonth) {
                dayClass += 'text-slate-300';
            } else if (isToday) {
                dayClass += 'bg-indigo-600 text-white shadow-md shadow-indigo-100';
            } else {
                dayClass += 'text-slate-700';
                if(cellDate.getDay() === 0) dayClass += ' text-rose-500';
                if(cellDate.getDay() === 6) dayClass += ' text-blue-500';
            }
            daySpan.className = dayClass;
            headerDiv.appendChild(daySpan);
            cell.appendChild(headerDiv);

            // 該当日の予約
            const dayReservations = reservations.filter(r => r.date === dateString)
                                                .sort((a, b) => a.time.localeCompare(b.time));
            
            const eventsContainer = document.createElement('div');
            eventsContainer.className = 'mt-1.5 flex-1 flex flex-col gap-1 overflow-y-auto max-h-[90px] no-scrollbar';
            
            dayReservations.forEach(res => {
                const eventItem = document.createElement('div');
                let bgColors = "bg-blue-50 text-blue-800 border-blue-100 hover:bg-blue-100";
                if(res.status === 'pending') bgColors = "bg-amber-50 text-amber-800 border-amber-100 hover:bg-amber-100";
                if(res.status === 'cancelled') bgColors = "bg-slate-100 text-slate-400 border-slate-200 line-through opacity-60";

                eventItem.className = `text-[10px] font-medium px-2 py-0.5 rounded-lg border truncate cursor-pointer transition-all ${bgColors}`;
                eventItem.innerHTML = `<span class="font-bold">${res.time}</span> ${res.customerName}`;
                
                eventItem.onclick = (e) => {
                    e.stopPropagation();
                    openModal('edit', res);
                };
                eventsContainer.appendChild(eventItem);
            });

            if (dayReservations.length > 0 && isOtherMonth === false) {
                 const countBadge = document.createElement('span');
                 countBadge.className = "text-[9px] font-bold text-slate-400 bg-slate-100 px-1.5 py-0.5 rounded-md";
                 countBadge.textContent = `${dayReservations.length}`;
                 headerDiv.appendChild(countBadge);
            }

            cell.appendChild(eventsContainer);
            return cell;
        }

        // --- 予約一覧描画（サイドバー） ---
        function renderReservationList(filterText = "") {
            let sortedRes = [...reservations].sort((a, b) => {
                if (a.date !== b.date) return a.date.localeCompare(b.date);
                return a.time.localeCompare(b.time);
            });

            if (filterText) {
                const lowerFilter = filterText.toLowerCase();
                sortedRes = sortedRes.filter(r => 
                    r.customerName.toLowerCase().includes(lowerFilter) || 
                    (r.contactInfo && r.contactInfo.includes(lowerFilter)) ||
                    (r.notes && r.notes.toLowerCase().includes(lowerFilter))
                );
            }

            const renderList = (container) => {
                container.innerHTML = '';
                
                if (sortedRes.length === 0) {
                    container.innerHTML = `
                        <div class="text-center py-10 text-slate-400">
                            <i class="fa-regular fa-folder-open text-3xl mb-2 text-slate-300"></i>
                            <p class="text-xs font-semibold">該当する予約がありません</p>
                        </div>`;
                    return;
                }

                let currentGrpDate = "";
                
                sortedRes.forEach(res => {
                    if (res.date !== currentGrpDate) {
                        currentGrpDate = res.date;
                        const dateObj = new Date(res.date);
                        const isToday = res.date === formatDateString(today);
                        
                        const dateHeader = document.createElement('div');
                        dateHeader.className = `text-xs font-bold px-3 py-1.5 mt-3 mb-1.5 sticky top-0 z-10 rounded-lg shadow-sm flex items-center justify-between ${isToday ? 'bg-indigo-600 text-white shadow-indigo-100' : 'bg-slate-100 text-slate-700'}`;
                        dateHeader.innerHTML = `
                            <span>${res.date.replace(/-/g, '/')} (${['日','月','火','水','木','金','土'][dateObj.getDay()]})</span>
                            ${isToday ? '<span class="text-[9px] bg-white text-indigo-600 font-extrabold px-1.5 rounded-full uppercase">Today</span>' : ''}
                        `;
                        container.appendChild(dateHeader);
                    }

                    const item = document.createElement('div');
                    const badgeClass = getStatusBadgeClass(res.status);
                    const statusText = getStatusText(res.status);
                    const isCancelled = res.status === 'cancelled';
                    
                    item.className = `bg-white p-3.5 rounded-xl border border-slate-200/80 shadow-sm hover:shadow-md hover:border-indigo-100 transition-all cursor-pointer flex flex-col gap-2 ${isCancelled ? 'opacity-60 bg-slate-50/50' : ''}`;
                    item.onclick = () => {
                        openModal('edit', res);
                        if(!mobileListOverlay.classList.contains('hidden')){
                            mobileListOverlay.classList.add('hidden');
                        }
                    };

                    item.innerHTML = `
                        <div class="flex justify-between items-start">
                            <div class="font-bold text-slate-800 text-sm ${isCancelled ? 'line-through text-slate-400' : ''}">${res.customerName}</div>
                            <span class="text-[9px] font-bold px-2 py-0.5 rounded-full border ${badgeClass}">${statusText}</span>
                        </div>
                        <div class="flex justify-between items-center text-xs text-slate-500">
                            <div class="flex items-center gap-1.5">
                                <i class="fa-regular fa-clock text-indigo-500"></i>
                                <span class="font-bold text-slate-700">${res.time}</span>
                            </div>
                            <div class="text-[10px] text-slate-500 font-bold bg-slate-100 px-1.5 py-0.5 rounded-md flex items-center gap-1">
                                <i class="fa-solid fa-user-group text-slate-400"></i> ${res.partySize}名
                            </div>
                        </div>
                        ${res.menu || res.staff ? `
                        <div class="text-[10px] mt-1 flex flex-wrap gap-1.5">
                            ${res.menu ? `<span class="bg-indigo-50 text-indigo-700 font-semibold px-2 py-0.5 rounded-md border border-indigo-100/50"><i class="fa-solid fa-bell-concierge mr-1 text-indigo-400"></i>${res.menu}</span>` : ''}
                            ${res.staff ? `<span class="bg-purple-50 text-purple-700 font-semibold px-2 py-0.5 rounded-md border border-purple-100/50"><i class="fa-solid fa-user-tag mr-1 text-purple-400"></i>${res.staff}</span>` : ''}
                        </div>` : ''}
                        ${res.notes ? `<div class="text-[10px] text-slate-400 italic line-clamp-1 mt-0.5"><i class="fa-regular fa-message mr-1"></i>${res.notes}</div>` : ''}
                        ${res.contactInfo ? `<div class="text-[10px] text-slate-400 border-t pt-1.5 border-slate-100 mt-1 flex items-center gap-1"><i class="fa-solid fa-phone text-slate-300"></i>${res.contactInfo}</div>` : ''}
                    `;
                    container.appendChild(item);
                });
            };

            renderList(reservationList);
            renderList(mobileReservationList);
        }

        searchInput.addEventListener('input', (e) => renderReservationList(e.target.value));
        mobileSearchInput.addEventListener('input', (e) => renderReservationList(e.target.value));

        // --- モーダル・フォーム制御 ---
        function openModal(mode, data = null) {
            const formModeInput = document.getElementById('formMode');
            const modalTitle = document.getElementById('modalTitle');
            
            formModeInput.value = mode;
            reservationForm.reset();
            aiInputText.value = "";
            
            // 返信作成UI初期化
            aiReplyOutputContainer.classList.add('hidden');
            aiReplyOutput.value = "";

            document.getElementById('resDate').value = formatDateString(today);
            
            if (mode === 'create') {
                modalTitle.textContent = '新規予約の登録';
                deleteReservationBtn.classList.add('hidden');
                document.getElementById('reservationId').value = "";
                modalTabsHeader.classList.remove('hidden'); // 新規作成時はAI自動入力タブを表示
                switchTab('manual');
                aiReplySection.classList.add('hidden'); // 新規は返信作成を隠す
            } else if (mode === 'edit' && data) {
                modalTitle.textContent = '予約の編集';
                deleteReservationBtn.classList.remove('hidden');
                modalTabsHeader.classList.add('hidden'); // 編集時はAI自動入力タブを隠す
                switchTab('manual');
                aiReplySection.classList.remove('hidden'); // 既存編集時は返信アシスタントを解放
                
                document.getElementById('reservationId').value = data.id;
                document.getElementById('customerName').value = data.customerName;
                document.getElementById('contactInfo').value = data.contactInfo || "";
                document.getElementById('resDate').value = data.date;
                document.getElementById('resTime').value = data.time;
                document.getElementById('partySize').value = data.partySize;
                document.getElementById('status').value = data.status;
                document.getElementById('menu').value = data.menu || "";
                document.getElementById('staff').value = data.staff || "";
                document.getElementById('notes').value = data.notes || "";
            }

            modal.classList.remove('hidden');
        }

        function closeModal() {
            modal.classList.add('hidden');
        }

        reservationForm.addEventListener('submit', (e) => {
            e.preventDefault();
            
            const mode = document.getElementById('formMode').value;
            const id = document.getElementById('reservationId').value;
            
            const formData = {
                customerName: document.getElementById('customerName').value,
                contactInfo: document.getElementById('contactInfo').value,
                date: document.getElementById('resDate').value,
                time: document.getElementById('resTime').value,
                partySize: parseInt(document.getElementById('partySize').value),
                status: document.getElementById('status').value,
                menu: document.getElementById('menu').value,
                staff: document.getElementById('staff').value,
                notes: document.getElementById('notes').value
            };

            if (mode === 'create') {
                const newId = 'res-' + Date.now();
                reservations.push({ id: newId, ...formData });
                showToast('予約を登録しました', 'success');
            } else if (mode === 'edit') {
                const index = reservations.findIndex(r => r.id === id);
                if (index !== -1) {
                    reservations[index] = { id, ...formData };
                    showToast('予約を更新しました', 'success');
                }
            }

            saveReservationsToStorage(); // 変更を自動保存
            renderCalendar(currentDate);
            renderReservationList();
            preloadSummary(); // リスト変更時にAI要約もバックグラウンドで再計算
            closeModal();
        });

        deleteReservationBtn.addEventListener('click', () => {
            const id = document.getElementById('reservationId').value;
            reservations = reservations.filter(r => r.id !== id);
            showToast('予約を削除しました', 'error');
            
            saveReservationsToStorage(); // 変更を自動保存
            renderCalendar(currentDate);
            renderReservationList();
            preloadSummary();
            closeModal();
        });

        // --- クリップボードコピー機能 ---
        function copyToClipboard() {
            const textarea = document.getElementById('aiReplyOutput');
            textarea.select();
            document.execCommand('copy');
            showToast("メッセージをクリップボードにコピーしました！", "success");
        }

        // --- データのPC保存（ダウンロード）機能 ---
        function exportReservations() {
            const dataStr = JSON.stringify(reservations, null, 2);
            const blob = new Blob([dataStr], { type: "application/json" });
            const url = URL.createObjectURL(blob);
            
            // 一時的にダウンロードリンクを作ってクリックさせる
            const tempLink = document.createElement('a');
            tempLink.href = url;
            tempLink.download = `reservation_backup_${formatDateString(today)}.json`;
            document.body.appendChild(tempLink);
            tempLink.click();
            
            // クリーンアップ
            document.body.removeChild(tempLink);
            URL.revokeObjectURL(url);
            
            showToast("PCへのバックアップ保存が完了しました！", "success");
        }

        // --- データのPCからの復元（インポート）機能 ---
        function importReservations(event) {
            const file = event.target.files[0];
            if (!file) return;

            const reader = new FileReader();
            reader.onload = function(e) {
                try {
                    const importedData = JSON.parse(e.target.result);
                    
                    // 最低限のバリデーション（配列かどうか）
                    if (Array.isArray(importedData)) {
                        reservations = importedData;
                        saveReservationsToStorage(); // ローカルストレージに書き込み
                        
                        renderCalendar(currentDate);
                        renderReservationList();
                        preloadSummary();
                        
                        showToast("バックアップから正常に復元しました！", "success");
                        dataManagementModal.classList.add('hidden');
                    } else {
                        throw new Error("フォーマットが予約データの配列ではありません。");
                    }
                } catch (error) {
                    console.error("インポートエラー:", error);
                    showToast("ファイルの復元に失敗しました。正しいバックアップ用ファイルかご確認ください。", "error");
                }
            };
            reader.readAsText(file);
        }

        // --- STREAMING_CHUNK: Registering DOM event listeners... ---
        function setupEventListeners() {
            prevMonthBtn.addEventListener('click', () => {
                currentDate.setMonth(currentDate.getMonth() - 1);
                renderCalendar(currentDate);
            });

            nextMonthBtn.addEventListener('click', () => {
                currentDate.setMonth(currentDate.getMonth() + 1);
                renderCalendar(currentDate);
            });

            todayBtn.addEventListener('click', () => {
                currentDate = new Date(today);
                renderCalendar(currentDate);
            });

            openModalBtn.addEventListener('click', () => openModal('create'));
            cancelModalBtn.addEventListener('click', closeModal);
            modalOverlay.addEventListener('click', closeModal);
            
            // データ管理関連のイベント
            dataManagementBtn.addEventListener('click', () => dataManagementModal.classList.remove('hidden'));
            dataManagementOverlay.addEventListener('click', () => dataManagementModal.classList.add('hidden'));
            closeDataModalBtn.addEventListener('click', () => dataManagementModal.classList.add('hidden'));
            exportBtn.addEventListener('click', exportReservations);
            importFile.addEventListener('change', importReservations);

            // AI自動パース関連イベント
            tabManual.addEventListener('click', () => switchTab('manual'));
            tabAi.addEventListener('click', () => switchTab('ai'));
            runAiExtractBtn.addEventListener('click', runAiExtraction);
            generateAiReplyBtn.addEventListener('click', runAiReplyGeneration);
            copyAiReplyBtn.addEventListener('click', copyToClipboard);

            // AIアドバイザーモーダルイベント
            aiAdvisorBtn.addEventListener('click', () => triggerDailySummary());
            aiAdvisorOverlay.addEventListener('click', () => aiAdvisorModal.classList.add('hidden'));
            closeAiAdvisorBtn.addEventListener('click', () => aiAdvisorModal.classList.add('hidden'));
            closeAiAdvisorBtn2.addEventListener('click', () => aiAdvisorModal.classList.add('hidden'));

            // モバイルビュー
            toggleListBtn.addEventListener('click', () => {
                mobileListOverlay.classList.remove('hidden');
                mobileListOverlay.classList.add('flex');
                setTimeout(() => {
                    mobileListOverlay.firstElementChild.classList.remove('translate-y-full');
                }, 10);
            });

            closeMobileListBtn.addEventListener('click', () => {
                mobileListOverlay.firstElementChild.classList.add('translate-y-full');
                setTimeout(() => {
                    mobileListOverlay.classList.add('hidden');
                    mobileListOverlay.classList.remove('flex');
                }, 300);
            });
        }

        const style = document.createElement('style');
        style.innerHTML = `
            .no-scrollbar::-webkit-scrollbar {
                display: none;
            }
            .no-scrollbar {
                -ms-overflow-style: none;
                scrollbar-width: none;
            }
        `;
        document.head.appendChild(style);

        window.addEventListener('DOMContentLoaded', init);
    </script>
</body>
</html>
