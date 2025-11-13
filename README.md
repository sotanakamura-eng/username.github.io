# username.github.io
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>警備事業 求人集客戦略レポート - 株式会社ロフティー様</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body {
            font-family: 'Inter', 'Noto Sans JP', sans-serif;
            background-color: #f8f9fa;
        }
        .tab-btn {
            transition: all 0.3s ease;
        }
        .tab-btn.active {
            border-bottom-color: #2563eb;
            color: #2563eb;
            font-weight: 600;
        }
        .tab-content {
            display: none;
        }
        .tab-content.active {
            display: block;
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
            height: 300px;
            max-height: 400px;
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }
    </style>
</head>
<body class="bg-gray-50 text-gray-800">
    <!-- Chosen Palette: Cool Blues and Neutrals -->
    <!-- Application Structure Plan: ユーザー（事業責任者）が戦略を直感的に理解できるよう、ダッシュボード型のSPAを設計。ナビゲーションは「戦略概要」「市場分析」「予算シミュレーション」「実行プラン」の4つのタブで構成。この構造により、①結論（推奨ポートフォリオ）、②根拠（市場動向）、③具体的な費用対効果（シミュレーション）、④次の行動（ToDo）という論理的な流れで情報を探索できるため、意思決定支援に最適と判断。 -->
    <!-- Visualization & Content Choices: 
        - [戦略概要]推奨ポートフォリオ: 予算配分の全体像を即座に把握する（Goal: Inform）。Chart.jsのドーナツグラフ（Viz/Presentation）を使用。インタラクションはホバー時のツールチップ（Interaction）。予算の大部分をクリック課金型に集中させる戦略を視覚化（Justification）。
        - [市場分析]エリア別CPC傾向: エリアごとのコスト感を比較する（Goal: Compare）。Chart.jsの棒グラフ（Viz/Presentation）を使用。各エリアの競合状況（ダミー傾向）を提示（Justification）。
        - [市場分析]メディア比較: メディア特性を整理する（Goal: Organize）。HTMLテーブル（Viz/Presentation）を使用。静的だが、戦略の根拠となる情報を一覧化（Justification）。
        - [予算シミュレーション]予算スライダーと連動グラフ: 予算の変動が配分と想定応募数にどう影響するか試算する（Goal: Change）。HTMLスライダーとJSによる数値更新（Viz/Presentation）。予算の柔軟性を体験させ、費用対効果を具体的にイメージさせる（Interaction/Justification）。
        - [実行プラン]ステップリスト: 次に取るべき行動を明確にする（Goal: Inform）。HTMLの順序付きリスト（Viz/Presentation）。戦略を具体的なタスクに落とし込む（Justification）。
        - 全てChart.js(Canvas)またはHTML/CSS/JSで実装。
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

    <div class="container mx-auto p-4 md:p-8 max-w-7xl">

        <header class="mb-8">
            <div class="flex flex-col md:flex-row justify-between items-start md:items-center">
                <div>
                    <h1 class="text-3xl font-bold text-gray-900">警備事業 求人集客戦略レポート</h1>
                    <p class="text-lg text-gray-600">株式会社ロフティー様（対象エリア：川越市・鶴ヶ島市・川口市）</p>
                </div>
                <div class="text-sm text-gray-500 mt-2 md:mt-0">2025年11月13日版</div>
            </div>
            
            <div class="mt-6 grid grid-cols-2 md:grid-cols-4 gap-4">
                <div class="bg-white p-4 rounded-lg shadow-sm border border-gray-200">
                    <span class="text-xs font-semibold text-gray-500 uppercase">対象エリア</span>
                    <p class="text-lg font-bold text-gray-800">川越市, 鶴ヶ島市, 川口市</p>
                </div>
                <div class="bg-white p-4 rounded-lg shadow-sm border border-gray-200">
                    <span class="text-xs font-semibold text-gray-500 uppercase">対象職種</span>
                    <p class="text-lg font-bold text-gray-800">常駐警備, 交通誘導・イベント警備</p>
                </div>
                <div class="bg-white p-4 rounded-lg shadow-sm border border-gray-200">
                    <span class="text-xs font-semibold text-gray-500 uppercase">月間予算</span>
                    <p class="text-lg font-bold text-blue-600">15万円 〜 20万円</p>
                </div>
                <div class="bg-white p-4 rounded-lg shadow-sm border border-gray-200">
                    <span class="text-xs font-semibold text-gray-500 uppercase">戦略ゴール</span>
                    <p class="text-lg font-bold text-gray-800">応募効果の最大化</p>
                </div>
            </div>
        </header>

        <main>
            <div class="border-b border-gray-300 mb-6">
                <nav class="-mb-px flex space-x-6 overflow-x-auto" aria-label="Tabs">
                    <button id="tab-btn-1" class="tab-btn active whitespace-nowrap py-3 px-1 border-b-2 font-medium text-sm text-gray-500 border-transparent hover:border-gray-400">
                        戦略概要
                    </button>
                    <button id="tab-btn-2" class="tab-btn whitespace-nowrap py-3 px-1 border-b-2 font-medium text-sm text-gray-500 border-transparent hover:border-gray-400">
                        市場・メディア分析
                    </button>
                    <button id="tab-btn-3" class="tab-btn whitespace-nowrap py-3 px-1 border-b-2 font-medium text-sm text-gray-500 border-transparent hover:border-gray-400">
                        予算シミュレーション
                    </button>
                    <button id="tab-btn-4" class="tab-btn whitespace-nowrap py-3 px-1 border-b-2 font-medium text-sm text-gray-500 border-transparent hover:border-gray-400">
                        実行アクションプラン
                    </button>
                </nav>
            </div>

            <div id="tab-content-1" class="tab-content active">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="bg-white p-6 rounded-lg shadow border border-gray-200">
                        <h2 class="text-xl font-semibold mb-4">推奨ポートフォリオ</h2>
                        <p class="text-gray-600 mb-4">ご予算（15〜20万円）と3エリアでの効果最大化を鑑み、予算の柔軟性と費用対効果（CPA）に優れる「クリック課金型（アグリゲーション）メディア」を戦略の主軸に据えることを強く推奨します。</p>
                        <div class="chart-container" style="height: 250px; max-height: 300px;">
                            <canvas id="portfolioChart"></canvas>
                        </div>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow border border-gray-200">
                        <h2 class="text-xl font-semibold mb-4">戦略のポイント</h2>
                        <div class="space-y-4">
                            <div>
                                <h3 class="font-semibold text-blue-700">1. 主軸: Indeed & 求人ボックス (予算の70-80%)</h3>
                                <p class="text-gray-600 text-sm">
                                    警備員の仕事を探す求職者の多くが利用する2大プラットフォームです。クリック課金（CPC）のため、関心のないユーザーへの露出コストは発生しません。3エリア・2職種それぞれで効果を測定し、応募単価（CPA）の良い求人へ動的に予算を集中させることが可能です。
                                </p>
                            </div>
                            <div>
                                <h3 class="font-semibold text-blue-700">2. 補完: 地域密着メディア (予算の20-30% + 無料)</h3>
                                <p class="text-gray-600 text-sm">
                                    主軸メディアでカバーしきれない層（特にシニア層や地元志向の主婦層など）へのアプローチとして活用します。
                                    <br>・<strong>ジモティー:</strong> 無料掲載が可能で、地域密着の応募（特に中高年層）が見込めます。
                                    <br>・<strong>テスト枠:</strong> 残予算で、地域フリーペーパーや大手求人サイトの廉価プラン（タウンワークネットなど）を短期で試し、効果を測定します。
                                </p>
                            </div>
                            <div>
                                <h3 class="font-semibold text-blue-700">3. 必須: 自社採用ページの最適化</h3>
                                <p class="text-gray-600 text-sm">
                                    広告クリック後の「受け皿」となる貴社採用ページが非常に重要です。エリア別・職種別に、仕事内容、給与、シフト、未経験者へのサポート体制が明確に伝わるよう整備する必要があります。
                                </p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <div id="tab-content-2" class="tab-content">
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                    <div class="bg-white p-6 rounded-lg shadow border border-gray-200">
                        <h2 class="text-xl font-semibold mb-4">エリア別 想定クリック単価（CPC）傾向</h2>
                        <p class="text-gray-600 mb-4">警備職種におけるクリック単価の傾向（推定）です。競合が多いエリア（川口市など）は単価が上がりやすいですが、運用調整により最適化が可能です。</p>
                        <div class="chart-container">
                            <canvas id="cpcChart"></canvas>
                        </div>
                    </div>
                    <div class="bg-white p-6 rounded-lg shadow border border-gray-200">
                        <h2 class="text-xl font-semibold mb-4">主要メディア特性比較</h2>
                        <div class="overflow-x-auto">
                            <table class="w-full text-left text-sm">
                                <thead class="bg-gray-100 text-gray-700 uppercase text-xs">
                                    <tr>
                                        <th class="py-3 px-4">メディア</th>
                                        <th class="py-3 px-4">課金形態</th>
                                        <th class="py-3 px-4">強み・特性</th>
                                        <th class="py-3 px-4">予算感（目安）</th>
                                    </tr>
                                </thead>
                                <tbody class="divide-y">
                                    <tr class="hover:bg-gray-50">
                                        <td class="py-3 px-4 font-semibold">Indeed</td>
                                        <td class="py-3 px-4">クリック課金</td>
                                        <td class="py-3 px-4">圧倒的な求職者数。詳細な運用調整が可能。</td>
                                        <td class="py-3 px-4">月5万〜（推奨10万〜）</td>
                                    </tr>
                                    <tr class="hover:bg-gray-50">
                                        <td class="py-3 px-4 font-semibold">求人ボックス</td>
                                        <td class="py-3 px-4">クリック課金</td>
                                        <td class="py-3 px-4">国内利用者数No.2。Indeedと併用で面を確保。</td>
                                        <td class="py-3 px-4">月3万〜（推奨5万〜）</td>
                                    </tr>
                                    <tr class="hover:bg-gray-50">
                                        <td class="py-3 px-4 font-semibold">タウンワーク等</td>
                                        <td class="py-3 px-4">掲載課金（枠）</td>
                                        <td class="py-3 px-4">若年層に強い。エリア・期間固定で露出。</td>
                                        <td class="py-3 px-4">月4万〜/1エリア枠</td>
                                    </tr>
                                    <tr class="hover:bg-gray-50">
                                        <td class="py-3 px-4 font-semibold">ジモティー</td>
                                        <td class="py-3 px-4">無料（一部有料）</td>
                                        <td class="py-3 px-4">地域密着。中高年・シニア層。費用ゼロ。</td>
                                        <td class="py-3 px-4">無料</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                        <p class="text-xs text-gray-500 mt-4">※掲載課金型（タウンワーク等）は、3エリア全てで掲載するとご予算（15-20万）の大半を消費するため、主軸には不向きと判断します。</p>
                    </div>
                </div>
            </div>

            <div id="tab-content-3" class="tab-content">
                <div class="bg-white p-6 rounded-lg shadow border border-gray-200">
                    <h2 class="text-xl font-semibold mb-4">月間予算シミュレーション</h2>
                    <p class="text-gray-600 mb-6">スライダーを動かして、総予算に応じた配分案と想定応募数（※）をご確認ください。主軸メディア（Indeed, 求人ボックス）に予算を集中させ、CPA（応募単価）を最適化するモデルです。</p>

                    <div class="mb-6">
                        <label for="budgetSlider" class="block text-sm font-medium text-gray-700">月間総予算: <span id="budgetValue" class="text-xl font-bold text-blue-600">17.5</span> 万円</label>
                        <input id="budgetSlider" type="range" min="15" max="20" value="17.5" step="0.5" class="w-full h-2 bg-gray-200 rounded-lg appearance-none cursor-pointer accent-blue-600">
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <div>
                            <h3 class="text-lg font-semibold mb-3">推奨予算配分</h3>
                            <div class="space-y-3">
                                <div>
                                    <div class="flex justify-between mb-1">
                                        <span class="text-sm font-medium text-gray-700">Indeed (主軸)</span>
                                        <span id="indeedBudget" class="text-sm font-medium text-gray-700">10.5 万円</span>
                                    </div>
                                    <div class="w-full bg-gray-200 rounded-full h-2.5">
                                        <div id="indeedBar" class="bg-blue-600 h-2.5 rounded-full" style="width: 60%"></div>
                                    </div>
                                </div>
                                <div>
                                    <div class="flex justify-between mb-1">
                                        <span class="text-sm font-medium text-gray-700">求人ボックス (主軸)</span>
                                        <span id="kugyoBudget" class="text-sm font-medium text-gray-700">3.5 万円</span>
                                    </div>
                                    <div class="w-full bg-gray-200 rounded-full h-2.5">
                                        <div id="kugyoBar" class="bg-blue-400 h-2.5 rounded-full" style="width: 20%"></div>
                                    </div>
                                </div>
                                <div>
                                    <div class="flex justify-between mb-1">
                                        <span class="text-sm font-medium text-gray-700">補完・テスト枠 (ジモティー含む)</span>
                                        <span id="otherBudget" class="text-sm font-medium text-gray-700">3.5 万円</span>
                                    </div>
                                    <div class="w-full bg-gray-200 rounded-full h-2.5">
                                        <div id="otherBar" class="bg-gray-400 h-2.5 rounded-full" style="width: 20%"></div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="bg-blue-50 border border-blue-200 p-6 rounded-lg text-center">
                            <h3 class="text-lg font-semibold text-gray-700">想定応募数（参考値）</h3>
                            <p id="estimatedApplicants" class="text-4xl font-bold text-blue-700 my-4">22 件</p>
                            <p class="text-xs text-gray-600">※想定CPA（応募単価）を 8,000円 と仮定した場合の試算です。実際のCPAは、求人原稿の魅力度、給与条件、競合状況、運用ノウハウによって大きく変動します。</p>
                        </div>
                    </div>
                </div>
            </div>

            <div id="tab-content-4" class="tab-content">
                <div class="bg-white p-6 rounded-lg shadow border border-gray-200">
                    <h2 class="text-xl font-semibold mb-6">実行アクションプラン（推奨ステップ）</h2>
                    <p class="text-gray-600 mb-6">戦略を成功させるため、以下のステップで進めることを推奨します。特に「1. 受け皿の整備」と「4. 効果測定」が重要です。</p>
                    <ol class="relative border-l border-gray-300 space-y-8 ml-4">
                        <li class="ml-6">
                            <span class="absolute flex items-center justify-center w-8 h-8 bg-blue-100 rounded-full -left-4 ring-4 ring-white">
                                <span class="font-bold text-blue-700">1</span>
                            </span>
                            <h3 class="text-lg font-semibold text-gray-900">基盤整備：採用ページの最適化</h3>
                            <p class="mt-1 text-sm text-gray-600">
                                広告をクリックした求職者が最初に着地するページ（貴社採用サイト）を整備します。
                                <br>・「川越」「鶴ヶ島」「川口」の勤務地情報
                                <br>・「常駐」「交通誘導」の具体的な仕事内容、給与、シフト
                                <br>・未経験者でも安心できる研修制度や、ロフティー様で働く魅力（安定性、資格支援など）を明記。
                            </p>
                        </li>
                        <li class="ml-6">
                            <span class="absolute flex items-center justify-center w-8 h-8 bg-blue-100 rounded-full -left-4 ring-4 ring-white">
                                <span class="font-bold text-blue-700">2</span>
                            </span>
                            <h3 class="text-lg font-semibold text-gray-900">主軸出稿：Indeed & 求人ボックス</h3>
                            <p class="mt-1 text-sm text-gray-600">
                                最適化した採用ページ（または求人原稿）を、Indeedと求人ボックスに有料出稿（スポンサー求人）します。
                                <br>・3エリア × 2職種（計6パターン以上）の求人を設定。
                                <br>・最初はクリック単価を低めに設定し、表示状況を見ながら調整します。
                            </p>
                        </li>
                        <li class="ml-6">
                            <span class="absolute flex items-center justify-center w-8 h-8 bg-blue-100 rounded-full -left-4 ring-4 ring-white">
                                <span class="font-bold text-blue-700">3</span>
                            </span>
                            <h3 class="text-lg font-semibold text-gray-900">補完出稿：ジモティー等</h3>
                            <p class="mt-1 text-sm text-gray-600">
                                ジモティーの「アルバイト」カテゴリに、3エリアそれぞれで無料掲載を開始します。反響があれば、補完・テスト枠の予算を使い、有料の地域メディアも試します。
                            </p>
                        </li>
                        <li class="ml-6">
                            <span class="absolute flex items-center justify-center w-8 h-8 bg-blue-100 rounded-full -left-4 ring-4 ring-white">
                                <span class="font-bold text-blue-700">4</span>
                            </span>
                            <h3 class="text-lg font-semibold text-gray-900">効果測定と改善（PDCA）</h3>
                            <p class="mt-1 text-sm text-gray-600">
                                <strong>[最重要]</strong> 毎週または隔週で、メディアごと・求人ごとの「表示回数」「クリック数」「応募数」「応募単価（CPA）」を必ず分析します。
                                <br>・応募単価が安い（効果の良い）求人・エリアに予算を寄せます。
                                <br>・効果の悪い求人は、原稿内容や単価設定を見直します。
                            </p>
                        </li>
                    </ol>
                </div>
            </div>
        </main>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const tabs = document.querySelectorAll('.tab-btn');
            const contents = document.querySelectorAll('.tab-content');

            tabs.forEach(tab => {
                tab.addEventListener('click', () => {
                    const target = tab.id.replace('tab-btn-', 'tab-content-');

                    tabs.forEach(t => t.classList.remove('active'));
                    tab.classList.add('active');

                    contents.forEach(c => c.classList.remove('active'));
                    document.getElementById(target).classList.add('active');
                });
            });

            const budgetSlider = document.getElementById('budgetSlider');
            const budgetValue = document.getElementById('budgetValue');
            const indeedBudget = document.getElementById('indeedBudget');
            const kugyoBudget = document.getElementById('kugyoBudget');
            const otherBudget = document.getElementById('otherBudget');
            const indeedBar = document.getElementById('indeedBar');
            const kugyoBar = document.getElementById('kugyoBar');
            const otherBar = document.getElementById('otherBar');
            const estimatedApplicants = document.getElementById('estimatedApplicants');
            
            const ASSUMED_CPA = 8000;

            function updateSimulation() {
                const totalBudget = parseFloat(budgetSlider.value);
                budgetValue.textContent = totalBudget.toFixed(1);

                const indeedRatio = 0.6;
                const kugyoRatio = 0.2;
                const otherRatio = 0.2;

                const indeedVal = totalBudget * indeedRatio;
                const kugyoVal = totalBudget * kugyoRatio;
                const otherVal = totalBudget * otherRatio;

                indeedBudget.textContent = `${indeedVal.toFixed(1)} 万円`;
                kugyoBudget.textContent = `${kugyoVal.toFixed(1)} 万円`;
                otherBudget.textContent = `${otherVal.toFixed(1)} 万円`;

                indeedBar.style.width = `${indeedRatio * 100}%`;
                kugyoBar.style.width = `${kugyoRatio * 100}%`;
                otherBar.style.width = `${otherRatio * 100}%`;

                const estimated = (totalBudget * 10000) / ASSUMED_CPA;
                estimatedApplicants.textContent = `${Math.round(estimated)} 件`;
            }

            budgetSlider.addEventListener('input', updateSimulation);
            
            updateSimulation();

            const portfolioCtx = document.getElementById('portfolioChart').getContext('2d');
            new Chart(portfolioCtx, {
                type: 'doughnut',
                data: {
                    labels: ['主軸: Indeed (60%)', '主軸: 求人ボックス (20%)', '補完: 地域・テスト枠 (20%)'],
                    datasets: [{
                        data: [60, 20, 20],
                        backgroundColor: ['#2563eb', '#60a5fa', '#9ca3af'],
                        borderColor: '#ffffff',
                        borderWidth: 2
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                padding: 15,
                                font: { size: 11 }
                            }
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return `${context.label}: ${context.raw}%`;
                                }
                            }
                        }
                    }
                }
            });

            const cpcCtx = document.getElementById('cpcChart').getContext('2d');
            new Chart(cpcCtx, {
                type: 'bar',
                data: {
                    labels: ['川口市（競合多）', '川越市（競合中）', '鶴ヶ島市（競合中）'],
                    datasets: [{
                        label: '想定CPC（クリック単価）傾向',
                        data: [120, 90, 85],
                        backgroundColor: ['#f87171', '#fbbf24', '#a3e635'],
                        borderRadius: 4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    indexAxis: 'y',
                    plugins: {
                        legend: { display: false },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return ` ${context.label}: ${context.raw} 円前後（推定）`;
                                }
                            }
                        }
                    },
                    scales: {
                        x: {
                            beginAtZero: true,
                            title: {
                                display: true,
                                text: '想定CPC（円）'
                            }
                        }
                    }
                }
            });
        });
    </script>
</body>
</html>
