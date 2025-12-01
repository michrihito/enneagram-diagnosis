[エニアグラム診断.html](https://github.com/user-attachments/files/23852896/default.html)
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>エニアグラムセンター診断</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { font-family: 'Helvetica Neue', Arial, 'Hiragino Kaku Gothic ProN', 'Hiragino Sans', Meiryo, sans-serif; }
        .fade-in { animation: fadeIn 0.5s ease-in; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
    </style>
</head>
<body class="bg-gradient-to-br from-blue-50 to-indigo-100 min-h-screen">
    <div id="app"></div>

    <script>
        const DATA = {
            questions: {
                high: [
                    { id: "h1", text: "困難な状況でも、自分の力で道を切り開いていける自信がある", center: "gut" },
                    { id: "h2", text: "自分の信念や価値観を貫くことに、誇りを感じる", center: "gut" },
                    { id: "h3", text: "物事を自分の意志でコントロールできている実感がある", center: "gut" },
                    { id: "h4", text: "正しいと思ったことは、周囲の反対があっても主張できる", center: "gut" },
                    { id: "h5", text: "目標に向かって、迷わず行動を起こすことができる", center: "gut" },
                    { id: "h6", text: "人との深いつながりや絆を、心から大切に思っている", center: "heart" },
                    { id: "h7", text: "自分は周囲から必要とされていると感じる", center: "heart" },
                    { id: "h8", text: "他者の気持ちに寄り添い、共感することが自然にできる", center: "heart" },
                    { id: "h9", text: "自分らしさを表現することに喜びを感じる", center: "heart" },
                    { id: "h10", text: "人から認められたり評価されることで、前向きな気持ちになれる", center: "heart" },
                    { id: "h11", text: "複雑な問題でも、冷静に分析して解決策を見つけられる", center: "head" },
                    { id: "h12", text: "新しい知識や情報を得ることに、ワクワクする", center: "head" },
                    { id: "h13", text: "将来の見通しを立て、計画的に物事を進めることが得意だ", center: "head" },
                    { id: "h14", text: "様々な可能性を想像し、柔軟に対応できる自分がいる", center: "head" },
                    { id: "h15", text: "論理的に考えることで、不安や心配を整理できる", center: "head" }
                ],
                low: [
                    { id: "l1", text: "自分の怒りや苛立ちを、うまくコントロールできないことがある", center: "gut" },
                    { id: "l2", text: "完璧でない自分や他人に対して、厳しく批判的になってしまう", center: "gut" },
                    { id: "l3", text: "物事が思い通りにいかないと、強い不満やストレスを感じる", center: "gut" },
                    { id: "l4", text: "自分の判断や行動に、自信が持てず迷いが生じる", center: "gut" },
                    { id: "l5", text: "周囲に対して攻撃的になったり、過度に支配的になることがある", center: "gut" },
                    { id: "l6", text: "他人からどう思われているか、過剰に気になってしまう", center: "heart" },
                    { id: "l7", text: "自分は価値がない存在だと感じることがある", center: "heart" },
                    { id: "l8", text: "拒絶されることへの恐れから、本音を隠してしまう", center: "heart" },
                    { id: "l9", text: "嫉妬や羨望の感情に、心が揺さぶられることがある", center: "heart" },
                    { id: "l10", text: "自分の感情に飲み込まれて、客観的に状況を見られなくなる", center: "heart" },
                    { id: "l11", text: "先のことを考えすぎて、不安や心配が止まらなくなる", center: "head" },
                    { id: "l12", text: "情報や知識を集めすぎて、かえって行動できなくなることがある", center: "head" },
                    { id: "l13", text: "最悪のシナリオばかり想像して、恐怖を感じる", center: "head" },
                    { id: "l14", text: "頭で考えすぎて、感情や直感を無視してしまう", center: "head" },
                    { id: "l15", text: "選択肢が多すぎると、決断できずに混乱してしまう", center: "head" }
                ],
                reverse: [
                    { id: "qR1", text: "衝動的に行動してしまい、後で後悔することが多い", center: "gut" },
                    { id: "qR2", text: "計画を立てても、すぐに変更したくなってしまう", center: "head" }
                ],
                value: [
                    { id: "vA", text: "A. 曖昧なまま進むこと", type: "gut" },
                    { id: "vB", text: "B. 自分の頑張りが伝わらないこと", type: "heart" },
                    { id: "vC", text: "C. 理解できないまま判断を求められること", type: "head" }
                ]
            },
            resultContent: {
                gut: {
                    name: "ガッツ", color: "red",
                    strengths: "強い意志力と実行力で目標を達成できる／正義感が強く、信念を貫く勇気がある／困難な状況でもリーダーシップを発揮できる",
                    weaknesses: "完璧主義で自他に厳しくなりすぎる／怒りや不満をコントロールしにくい／柔軟性に欠け、妥協が苦手",
                    environment: "成果主義で評価が明確な職場、裁量権が大きいポジション、改善や変革を推進できる環境",
                    lowPattern: "コントロールを失うことへの恐れから、過度に支配的になったり、批判的になります。完璧でない状況に強いストレスを感じやすくなります。",
                    stagnation: "物事が思い通りにいかない時、または自分の基準に達していないと感じる時に、怒りや不満が高まり、行動が硬直化します。",
                    advice: "明確な目標と責任範囲を持ち、自分の判断で進められる環境が最適です。完璧主義を緩め、「80%で良し」とする柔軟性を持つことで、より高いパフォーマンスを発揮できます。"
                },
                heart: {
                    name: "ハート", color: "green",
                    strengths: "人の感情を理解し、深い信頼関係を築ける／共感力が高く、チームの調和を保てる／自己表現が豊かで、人を惹きつける魅力がある",
                    weaknesses: "他人の評価を気にしすぎて本音を隠す／拒絶や孤立への恐れが強い／感情に振り回されて客観性を失いやすい",
                    environment: "チームワークを重視する職場、感謝や承認の文化がある環境、人の成長や幸せに貢献できる仕事",
                    lowPattern: "承認欲求が満たされないと、自己価値を見失い、嫉妬や羨望に苦しみます。他者の反応に過敏になり、本来の自分を見失います。",
                    stagnation: "認められていないと感じる時、または人間関係で拒絶されたと感じる時に、感情的になり、冷静な判断ができなくなります。",
                    advice: "人との関わりが多く、貢献が目に見える環境が最適です。定期的なフィードバックを受けられる体制を整え、感情と事実を分けて考える習慣をつけると良いでしょう。"
                },
                head: {
                    name: "ヘッド", color: "blue",
                    strengths: "論理的思考で複雑な問題を解決できる／情報収集と分析が得意で、戦略的に動ける／多様な視点を持ち、柔軟に対応できる",
                    weaknesses: "考えすぎて行動に移せない／不安や心配が止まらなくなる／感情や直感を軽視してしまう",
                    environment: "知的好奇心を刺激される職場、データや分析を重視する環境、計画的に進められるプロジェクト",
                    lowPattern: "不確実性への恐怖から、過剰に情報を集め、最悪のシナリオばかり想像します。分析麻痺に陥り、決断できなくなります。",
                    stagnation: "先が見えない状況や、情報が不足していると感じる時に、不安が高まり、思考の堂々巡りに陥ります。",
                    advice: "学習機会が豊富で、専門性を深められる環境が最適です。「完璧な答え」を求めすぎず、「60%で動く」勇気を持つことで、より効果的に働けます。"
                }
            }
        };

        let STATE = {
            page: 'intro',
            name: '', university: '', email: '',
            answers: {}, highMotivation: '', lowMotivation: '',
            result: null
        };

        function render() {
            const app = document.getElementById('app');
            if (STATE.page === 'intro') app.innerHTML = renderIntro();
            else if (STATE.page === 'diagnosis') app.innerHTML = renderDiagnosis();
            else if (STATE.page === 'result') app.innerHTML = renderResult();
            attachListeners();
        }

        function renderIntro() {
            return `
                <div class="fade-in py-12 px-4">
                    <div class="max-w-4xl mx-auto bg-white rounded-2xl shadow-xl p-8 md:p-12">
                        <h1 class="text-4xl md:text-5xl font-bold text-center text-indigo-900 mb-8">エニアグラムセンター診断</h1>
                        
                        <div class="prose prose-lg max-w-none mb-8 space-y-6">
                            <div class="bg-indigo-50 rounded-lg p-6">
                                <h2 class="text-2xl font-bold text-indigo-900 mb-3">【このワークの目的】</h2>
                                <p class="text-gray-700 leading-relaxed">このワークは、あなたの本質的な判断基準や行動パターンを知るためのものです。</p>
                                <p class="text-gray-700 leading-relaxed mt-3">就職活動では「自分に合う会社を選ぶ」ことが重要ですが、多くの学生が"何が自分に合うのか"を言語化できずに悩みます。</p>
                                <ul class="list-disc list-inside space-y-2 mt-4 text-gray-700">
                                    <li>給料や福利厚生だけで選んでいいのか？</li>
                                    <li>「やりがい」って結局どういう状態？</li>
                                    <li>面接で「なぜこの会社か」を納得感を持って語れない…</li>
                                </ul>
                                <p class="text-gray-700 leading-relaxed mt-4">こうした悩みの正体は、<strong>"自分の判断の軸がどこにあるのか"を理解できていないこと</strong>が原因です。</p>
                                <p class="text-gray-700 leading-relaxed mt-3">このワークでは、エニアグラムの３つのセンター（ガッツ / ハート / ヘッド）を使って、あなたの「判断の軸」を可視化します。</p>
                            </div>

                            <div class="bg-green-50 rounded-lg p-6">
                                <h2 class="text-2xl font-bold text-green-900 mb-3">【診断するとわかること】</h2>
                                <ul class="space-y-3 text-gray-700">
                                    <li class="flex items-start"><span class="text-green-600 mr-2 text-xl">✓</span><span><strong>就活の軸：</strong>あなたが働く上で本当に大切にしている価値観</span></li>
                                    <li class="flex items-start"><span class="text-green-600 mr-2 text-xl">✓</span><span><strong>会社選びの基準：</strong>どんな環境で力を発揮できるのか</span></li>
                                    <li class="flex items-start"><span class="text-green-600 mr-2 text-xl">✓</span><span><strong>自己PR／志望動機：</strong>なぜその会社を選んだのかを自然に説明できる</span></li>
                                </ul>
                            </div>

                            <div class="bg-yellow-50 rounded-lg p-6 text-center">
                                <p class="text-gray-800 font-semibold text-lg">正解・不正解はありません。<br>直感で「自分はこうだ」と感じるものを選んでください。</p>
                            </div>
                        </div>

                        <div class="space-y-4 mb-8">
                            <div>
                                <label class="block text-sm font-bold text-gray-700 mb-2">氏名 *</label>
                                <input type="text" id="name" value="${STATE.name}" 
                                    class="w-full px-4 py-3 border-2 border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500"
                                    placeholder="山田太郎">
                            </div>
                            <div>
                                <label class="block text-sm font-bold text-gray-700 mb-2">大学 *</label>
                                <input type="text" id="university" value="${STATE.university}"
                                    class="w-full px-4 py-3 border-2 border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500"
                                    placeholder="○○大学">
                            </div>
                            <div>
                                <label class="block text-sm font-bold text-gray-700 mb-2">メールアドレス *</label>
                                <input type="email" id="email" value="${STATE.email}"
                                    class="w-full px-4 py-3 border-2 border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500"
                                    placeholder="example@email.com">
                            </div>
                        </div>

                        <div class="text-center">
                            <button id="startBtn" class="bg-indigo-600 text-white px-12 py-4 rounded-xl font-bold text-lg hover:bg-indigo-700 transition transform hover:scale-105 shadow-lg">
                                診断を開始する →
                            </button>
                        </div>
                    </div>
                </div>
            `;
        }

        function renderDiagnosis() {
            const allQ = [...DATA.questions.high, ...DATA.questions.low, ...DATA.questions.reverse];
            const allAnswered = allQ.every(q => STATE.answers[q.id] !== undefined) && STATE.answers.valueAnswer;
            
            return `
                <div class="fade-in py-12 px-4">
                    <div class="max-w-4xl mx-auto bg-white rounded-2xl shadow-xl p-8">
                        <h1 class="text-3xl font-bold text-center text-indigo-900 mb-2">診断質問</h1>
                        <p class="text-center text-gray-600 mb-8">各質問に対して、最も当てはまる選択肢を選んでください</p>
                        
                        <div class="mb-6 bg-indigo-50 rounded-lg p-4">
                            <p class="text-sm font-semibold text-indigo-900">回答の目安</p>
                            <div class="grid grid-cols-2 md:grid-cols-4 gap-2 mt-2 text-xs text-gray-700">
                                <div>1: まったく当てはまらない</div>
                                <div>2: あまり当てはまらない</div>
                                <div>3: やや当てはまる</div>
                                <div>4: とても当てはまる</div>
                            </div>
                        </div>

                        <div class="space-y-5">
                            ${allQ.map((q, i) => `
                                <div class="bg-gray-50 rounded-lg p-4 border-l-4 ${i < 15 ? 'border-green-400' : i < 30 ? 'border-orange-400' : 'border-purple-400'}">
                                    <p class="font-semibold text-gray-800 mb-3 text-sm md:text-base">Q${i + 1}. ${q.text}</p>
                                    <div class="grid grid-cols-4 gap-2">
                                        ${[1, 2, 3, 4].map(v => `
                                            <label class="flex flex-col items-center cursor-pointer p-2 rounded transition ${STATE.answers[q.id] === v ? 'bg-indigo-600 text-white' : 'bg-white hover:bg-gray-100'}">
                                                <input type="radio" name="${q.id}" value="${v}" ${STATE.answers[q.id] === v ? 'checked' : ''} class="hidden">
                                                <span class="text-lg font-bold">${v}</span>
                                            </label>
                                        `).join('')}
                                    </div>
                                </div>
                            `).join('')}
                        </div>

                        <div class="mt-8 bg-yellow-50 rounded-lg p-6 border-2 border-yellow-300">
                            <h3 class="text-xl font-bold text-gray-800 mb-3">価値観質問</h3>
                            <p class="font-semibold text-gray-800 mb-4">以下の中で、<strong>最も避けたいと感じるもの</strong>を1つ選んでください</p>
                            <div class="space-y-2">
                                ${DATA.questions.value.map(v => `
                                    <label class="flex items-center cursor-pointer p-3 rounded transition ${STATE.answers.valueAnswer === v.type ? 'bg-indigo-600 text-white' : 'bg-white hover:bg-gray-100'}">
                                        <input type="radio" name="value" value="${v.type}" ${STATE.answers.valueAnswer === v.type ? 'checked' : ''} class="hidden">
                                        <span class="font-medium">${v.text}</span>
                                    </label>
                                `).join('')}
                            </div>
                        </div>

                        <div class="mt-8 text-center">
                            <button id="resultBtn" ${!allAnswered ? 'disabled' : ''} 
                                class="${allAnswered ? 'bg-indigo-600 hover:bg-indigo-700' : 'bg-gray-400 cursor-not-allowed'} text-white px-12 py-4 rounded-xl font-bold text-lg transition shadow-lg">
                                結果を見る
                            </button>
                        </div>
                    </div>
                </div>
            `;
        }

        function renderResult() {
            const r = STATE.result;
            const colorMap = { red: 'bg-red-500', green: 'bg-green-500', blue: 'bg-blue-500' };
            const textColorMap = { red: 'text-red-900', green: 'text-green-900', blue: 'text-blue-900' };
            
            return `
                <div class="fade-in py-12 px-4">
                    <div class="max-w-5xl mx-auto bg-white rounded-2xl shadow-xl p-8">
                        <h1 class="text-4xl font-bold text-center text-indigo-900 mb-8">診断結果</h1>
                        
                        <div class="bg-gradient-to-r from-indigo-100 to-purple-100 rounded-xl p-8 mb-8 text-center">
                            <h2 class="text-2xl font-bold text-gray-800 mb-4">あなたは</h2>
                            <div class="text-6xl font-bold ${textColorMap[r.color]} mb-2">${r.name}センター</div>
                            <p class="text-gray-700 text-lg">です</p>
                        </div>

                        <div class="mb-8">
                            <h3 class="text-xl font-bold text-gray-800 mb-4 text-center">センターのスコア</h3>
                            <div class="grid md:grid-cols-3 gap-4">
                                <div class="bg-red-50 rounded-lg p-6 text-center border-2 ${r.centerType === 'gut' ? 'border-red-500' : 'border-transparent'}">
                                    <div class="text-sm font-bold text-red-900 mb-2">ガッツ</div>
                                    <div class="text-4xl font-bold text-red-600">${r.gutScore}</div>
                                    <div class="mt-2 bg-red-200 rounded-full h-2">
                                        <div class="bg-red-600 h-2 rounded-full" style="width: ${Math.min(100, (r.gutScore / 50) * 100)}%"></div>
                                    </div>
                                </div>
                                <div class="bg-green-50 rounded-lg p-6 text-center border-2 ${r.centerType === 'heart' ? 'border-green-500' : 'border-transparent'}">
                                    <div class="text-sm font-bold text-green-900 mb-2">ハート</div>
                                    <div class="text-4xl font-bold text-green-600">${r.heartScore}</div>
                                    <div class="mt-2 bg-green-200 rounded-full h-2">
                                        <div class="bg-green-600 h-2 rounded-full" style="width: ${Math.min(100, (r.heartScore / 50) * 100)}%"></div>
                                    </div>
                                </div>
                                <div class="bg-blue-50 rounded-lg p-6 text-center border-2 ${r.centerType === 'head' ? 'border-blue-500' : 'border-transparent'}">
                                    <div class="text-sm font-bold text-blue-900 mb-2">ヘッド</div>
                                    <div class="text-4xl font-bold text-blue-600">${r.headScore}</div>
                                    <div class="mt-2 bg-blue-200 rounded-full h-2">
                                        <div class="bg-blue-600 h-2 rounded-full" style="width: ${Math.min(100, (r.headScore / 50) * 100)}%"></div>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <div class="space-y-6">
                            <div class="bg-green-50 rounded-lg p-6 border-l-4 border-green-500">
                                <h3 class="text-xl font-bold text-green-900 mb-3">強み</h3>
                                ${r.strengths.split('／').map(s => `<p class="text-gray-700 mb-2 flex items-start"><span class="text-green-600 mr-2">✓</span><span>${s}</span></p>`).join('')}
                            </div>

                            <div class="bg-orange-50 rounded-lg p-6 border-l-4 border-orange-500">
                                <h3 class="text-xl font-bold text-orange-900 mb-3">弱み</h3>
                                ${r.weaknesses.split('／').map(w => `<p class="text-gray-700 mb-2 flex items-start"><span class="text-orange-600 mr-2">▲</span><span>${w}</span></p>`).join('')}
                            </div>

                            <div class="bg-indigo-50 rounded-lg p-6 border-l-4 border-indigo-500">
                                <h3 class="text-xl font-bold text-indigo-900 mb-3">相性の良い職場環境</h3>
                                <p class="text-gray-700">${r.environment}</p>
                            </div>

                            <div class="bg-gray-50 rounded-lg p-6 border-l-4 border-gray-500">
                                <h3 class="text-xl font-bold text-gray-900 mb-3">低調パターン</h3>
                                <p class="text-gray-700">${r.lowPattern}</p>
                            </div>

                            <div class="bg-gray-50 rounded-lg p-6 border-l-4 border-gray-500">
                                <h3 class="text-xl font-bold text-gray-900 mb-3">停滞ポイント</h3>
                                <p class="text-gray-700">${r.stagnation}</p>
                            </div>

                            <div class="bg-purple-50 rounded-lg p-6 border-l-4 border-purple-500">
                                <h3 class="text-xl font-bold text-purple-900 mb-3">ワンポイントメモ</h3>
                                <p class="text-gray-700">${r.advice}</p>
                            </div>
                        </div>

                        <div class="mt-8 bg-yellow-50 rounded-lg p-6 border-2 border-yellow-400">
                            <h3 class="text-xl font-bold text-gray-800 mb-3">振り返り</h3>
                            <p class="text-gray-700 mb-4">過去のアルバイトや部活などの経験を振り返って、自分が気持ちよく動ける環境とそうでない環境を書いてください。</p>
                            
                            <div class="mb-4">
                                <label class="block text-sm font-bold text-gray-700 mb-2">モチベーションが高かった場面</label>
                                <textarea id="highMotivation" rows="4" 
                                    class="w-full px-4 py-3 border-2 border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500"
                                    placeholder="例：アルバイトでリーダーを任された時は責任感を持って取り組めた...">${STATE.highMotivation || ''}</textarea>
                            </div>
                            
                            <div>
                                <label class="block text-sm font-bold text-gray-700 mb-2">モチベーションが低かった場面</label>
                                <textarea id="lowMotivation" rows="4" 
                                    class="w-full px-4 py-3 border-2 border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-indigo-500"
                                    placeholder="例：指示待ちの環境では物足りなさを感じた...">${STATE.lowMotivation || ''}</textarea>
                            </div>
                        </div>

                        <div class="mt-8 text-center">
                            <button id="submitBtn" class="bg-indigo-600 text-white px-12 py-4 rounded-xl font-bold text-lg hover:bg-indigo-700 transition shadow-lg">
                                結果を送信する
                            </button>
                        </div>
                    </div>
                </div>
            `;
        }

        function attachListeners() {
            if (STATE.page === 'intro') {
                ['name', 'university', 'email'].forEach(id => {
                    const el = document.getElementById(id);
                    if (el) el.addEventListener('input', e => { STATE[id] = e.target.value; });
                });
                const btn = document.getElementById('startBtn');
                if (btn) btn.addEventListener('click', () => {
                    if (!STATE.name || !STATE.university || !STATE.email) {
                        alert('すべての項目を入力してください');
                        return;
                    }
                    STATE.page = 'diagnosis';
                    render();
                    window.scrollTo(0, 0);
                });
            } else if (STATE.page === 'diagnosis') {
                const allQ = [...DATA.questions.high, ...DATA.questions.low, ...DATA.questions.reverse];
                allQ.forEach(q => {
                    document.querySelectorAll(`input[name="${q.id}"]`).forEach(inp => {
                        inp.addEventListener('change', e => {
                            STATE.answers[q.id] = parseInt(e.target.value);
                            render();
                        });
                    });
                });
                document.querySelectorAll('input[name="value"]').forEach(inp => {
                    inp.addEventListener('change', e => {
                        STATE.answers.valueAnswer = e.target.value;
                        render();
                    });
                });
                const btn = document.getElementById('resultBtn');
                if (btn && !btn.disabled) {
                    btn.addEventListener('click', () => {
                        calculateResult();
                        STATE.page = 'result';
                        render();
                        window.scrollTo(0, 0);
                    });
                }
            } else if (STATE.page === 'result') {
                const highMotiv = document.getElementById('highMotivation');
                const lowMotiv = document.getElementById('lowMotivation');
                if (highMotiv) highMotiv.addEventListener('input', e => { STATE.highMotivation = e.target.value; });
                if (lowMotiv) lowMotiv.addEventListener('input', e => { STATE.lowMotivation = e.target.value; });
                const btn = document.getElementById('submitBtn');
                if (btn) btn.addEventListener('click', sendToGoogle);
            }
        }

        function calculateResult() {
            let gutH = 0, gutL = 0, heartH = 0, heartL = 0, headH = 0, headL = 0;
            
            DATA.questions.high.forEach(q => {
                const v = (STATE.answers[q.id] || 1) - 1; // 1-4を0-3に変換
                if (q.center === 'gut') gutH += v;
                if (q.center === 'heart') heartH += v;
                if (q.center === 'head') headH += v;
            });
            
            DATA.questions.low.forEach(q => {
                const v = ((STATE.answers[q.id] || 1) - 1) * 1.3; // 1-4を0-3に変換して1.3倍
                if (q.center === 'gut') gutL += v;
                if (q.center === 'heart') heartL += v;
                if (q.center === 'head') headL += v;
            });
            
            const revGut = 3 - ((STATE.answers['qR1'] || 1) - 1);
            const revHead = 3 - ((STATE.answers['qR2'] || 1) - 1);
            gutH += revGut;
            headH += revHead;
            
            if (STATE.answers.valueAnswer === 'gut') gutH += 1;
            else if (STATE.answers.valueAnswer === 'heart') heartH += 1;
            else if (STATE.answers.valueAnswer === 'head') headH += 1;
            
            const gutTotal = gutH + gutL;
            const heartTotal = heartH + heartL;
            const headTotal = headH + headL;
            
            const maxScore = Math.max(gutTotal, heartTotal, headTotal);
            const maxCenters = [];
            if (gutTotal === maxScore) maxCenters.push('gut');
            if (heartTotal === maxScore) maxCenters.push('heart');
            if (headTotal === maxScore) maxCenters.push('head');
            
            let centerType = maxCenters[0];
            if (maxCenters.length > 1) {
                const vMap = { A: 'gut', B: 'heart', C: 'head' };
                const vAnswer = STATE.answers.valueAnswer;
                for (let c of maxCenters) {
                    if (vMap[vAnswer] === c) { centerType = c; break; }
                }
            }
            
            const consistency = Math.abs(gutTotal - heartTotal) + Math.abs(heartTotal - headTotal) + Math.abs(headTotal - gutTotal);
            const content = DATA.resultContent[centerType];
            
            STATE.result = {
                centerType, ...content,
                gutScore: gutTotal.toFixed(1),
                heartScore: heartTotal.toFixed(1),
                headScore: headTotal.toFixed(1),
                consistencyScore: consistency.toFixed(1)
            };
        }

        function sendToGoogle() {
            const r = STATE.result;
            
            const params = new URLSearchParams({
                'entry.2122251360': STATE.name,
                'entry.410900907': STATE.university,
                'entry.110905313': STATE.email,
                'entry.1724907639': r.name + 'センター',
                'entry.160120501': r.gutScore,
                'entry.1689316600': r.heartScore,
                'entry.2083436459': r.headScore,
                'entry.1179669840': STATE.highMotivation,
                'entry.990890573': STATE.lowMotivation
            });
            
            const url = `https://docs.google.com/forms/d/e/1FAIpQLSeejTVQTXHFDaCNrWAOtgR-ls7ciLuLKJiZuy8Wr_c01-_2NA/formResponse?${params.toString()}`;
            window.open(url, '_blank');
            
            setTimeout(() => {
                alert('結果を送信しました！ありがとうございました。');
            }, 500);
        }

        render();
    </script>
</body>
</html>
