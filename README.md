<!DOCTYPE html>
<html lang="tr" class="h-full">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>7. Sınıf Fen Bilgisi — Kuvvet ve Enerji Interaktif Testi</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.16.8/dist/katex.min.css">
  <script defer src="https://cdn.jsdelivr.net/npm/katex@0.16.8/dist/katex.min.js"></script>
  <script defer src="https://cdn.jsdelivr.net/npm/katex@0.16.8/dist/contrib/auto-render.min.js"></script>
  <style>
    @import url("https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap");
    body { font-family: "Inter", system-ui, sans-serif; }
    .custom-scrollbar::-webkit-scrollbar { width: 6px; height: 6px; }
    .custom-scrollbar::-webkit-scrollbar-track { background: #0f172a; }
    .custom-scrollbar::-webkit-scrollbar-thumb { background: #475569; border-radius: 4px; }
    button:focus-visible { outline: 2px solid #818cf8; outline-offset: 2px; }
  </style>
</head>
<body class="bg-slate-900 text-slate-100 min-h-full flex flex-col antialiased">
  <header class="bg-slate-800/90 backdrop-blur-md border-b border-slate-700/80 sticky top-0 z-30">
    <div class="max-w-5xl mx-auto px-4 py-3 flex justify-between items-center gap-3">
      <div class="flex items-center space-x-3 min-w-0">
        <div class="w-10 h-10 rounded-xl bg-gradient-to-tr from-indigo-500 to-purple-500 flex items-center justify-center text-xl shadow-lg shadow-indigo-500/30" aria-hidden="true">⚡</div>
        <div class="min-w-0">
          <h1 class="text-base md:text-lg font-bold text-white leading-tight truncate">7. Sınıf Fen Bilgisi</h1>
          <p class="text-xs text-indigo-400 font-medium">Kuvvet ve Enerjiyi Keşfedelim</p>
        </div>
      </div>
      <div id="stats-header" class="hidden items-center space-x-2 md:space-x-4" aria-live="polite">
        <div class="bg-emerald-500/10 border border-emerald-500/30 text-emerald-400 text-xs font-semibold px-2.5 py-1 rounded-lg">
          ✓ <span id="score-correct-badge">0</span>
        </div>
        <div class="bg-rose-500/10 border border-rose-500/30 text-rose-400 text-xs font-semibold px-2.5 py-1 rounded-lg">
          ✗ <span id="score-wrong-badge">0</span>
        </div>
        <div class="bg-indigo-600 text-white text-xs font-bold px-3 py-1.5 rounded-lg">
          Soru: <span id="current-q-num">1</span>/30
        </div>
      </div>
    </div>
  </header>

  <main class="max-w-5xl mx-auto px-4 py-6 w-full flex-grow flex items-center justify-center">
    <section id="welcome-screen" class="bg-slate-800 border border-slate-700/80 rounded-3xl shadow-2xl p-6 md:p-10 max-w-xl w-full text-center relative overflow-hidden">
      <div class="absolute -right-10 -top-10 w-40 h-40 bg-indigo-500/10 rounded-full blur-2xl" aria-hidden="true"></div>
      <div class="w-20 h-20 bg-indigo-500/20 border border-indigo-500/30 text-indigo-400 rounded-2xl flex items-center justify-center mx-auto mb-6 text-4xl">🚀</div>
      <h2 class="text-2xl md:text-3xl font-extrabold text-white mb-3">Kuvvet ve Enerji Testi</h2>
     
      <button id="start-btn" type="button" class="w-full bg-gradient-to-r from-indigo-500 to-purple-600 hover:from-indigo-600 hover:to-purple-700 text-white font-bold py-4 px-6 rounded-xl shadow-lg shadow-indigo-500/25">
        Teste Başla
      </button>
    </section>

    <section id="quiz-screen" class="hidden w-full max-w-3xl bg-slate-800 rounded-3xl shadow-2xl border border-slate-700/80 p-5 md:p-8 flex-col justify-between" aria-label="Soru ekranı">
      <div>
        <div class="flex items-center justify-between mb-4">
          <span class="text-xs font-semibold px-3 py-1 rounded-full bg-indigo-500/10 border border-indigo-500/30 text-indigo-400">Ünite 3: Kuvvet ve Enerji</span>
          <span id="answered-status" class="text-xs text-slate-400 font-medium">Cevaplanmadı</span>
        </div>
        <div class="w-full bg-slate-900 rounded-full h-2 mb-6 overflow-hidden" role="progressbar" aria-valuemin="1" aria-valuemax="30" aria-valuenow="1">
          <div id="progress-bar" class="bg-gradient-to-r from-indigo-500 to-purple-500 h-2 rounded-full transition-all duration-300" style="width: 3.33%"></div>
        </div>
        <div id="question-grid" class="flex flex-wrap gap-1.5 mb-6 custom-scrollbar max-h-28 overflow-y-auto p-1 bg-slate-900/40 rounded-xl border border-slate-700/40" role="navigation" aria-label="Soru atlama"></div>
        <h3 id="question-text" class="text-base md:text-lg font-semibold text-slate-100 leading-relaxed mb-6">Soru yükleniyor...</h3>
        <div id="options-container" class="space-y-3 mb-6" role="list"></div>
        <div id="feedback-banner" class="hidden p-4 rounded-xl border mb-6" role="status"></div>
      </div>
      <div class="flex justify-between items-center pt-4 border-t border-slate-700/80">
        <button id="prev-btn" type="button" class="px-4 py-2.5 text-slate-400 hover:text-white font-medium text-sm disabled:opacity-30 disabled:cursor-not-allowed">← Önceki</button>
        <p class="text-xs text-slate-500 hidden sm:block">← → ok tuşları · A–D şık seçimi</p>
        <button id="next-btn" type="button" class="bg-indigo-600 hover:bg-indigo-500 text-white px-6 py-2.5 rounded-xl font-semibold text-sm shadow-lg shadow-indigo-600/30">Sonraki →</button>
      </div>
    </section>

    <section id="result-screen" class="hidden bg-slate-800 border border-slate-700/80 rounded-3xl shadow-2xl p-6 md:p-10 max-w-xl w-full text-center">
      <div id="result-icon" class="w-20 h-20 bg-emerald-500/20 border border-emerald-500/30 text-emerald-400 rounded-2xl flex items-center justify-center mx-auto mb-4 text-4xl">🏆</div>
      <h2 class="text-2xl md:text-3xl font-extrabold text-white mb-1">Test Tamamlandı!</h2>
      <p id="result-feedback-text" class="text-slate-400 text-sm mb-6">Tebrikler, tüm soruları yanıtladınız.</p>
      <div class="grid grid-cols-3 gap-3 mb-6">
        <div class="bg-slate-900/80 border border-emerald-500/30 p-4 rounded-2xl">
          <span id="score-correct" class="block text-2xl md:text-3xl font-black text-emerald-400">0</span>
          <span class="text-xs text-slate-400">Doğru</span>
        </div>
        <div class="bg-slate-900/80 border border-rose-500/30 p-4 rounded-2xl">
          <span id="score-wrong" class="block text-2xl md:text-3xl font-black text-rose-400">0</span>
          <span class="text-xs text-slate-400">Yanlış</span>
        </div>
        <div class="bg-slate-900/80 border border-amber-500/30 p-4 rounded-2xl">
          <span id="score-empty" class="block text-2xl md:text-3xl font-black text-amber-400">0</span>
          <span class="text-xs text-slate-400">Boş</span>
        </div>
      </div>
      <div class="mb-8 text-left bg-slate-900/60 border border-slate-700/60 p-4 rounded-2xl">
        <div class="flex justify-between text-xs font-semibold text-slate-300 mb-2">
          <span>Başarı yüzdesi</span>
          <span id="accuracy-percentage">0%</span>
        </div>
        <div class="w-full bg-slate-800 rounded-full h-3 overflow-hidden">
          <div id="accuracy-bar" class="bg-gradient-to-r from-emerald-500 to-indigo-500 h-3 rounded-full transition-all duration-500" style="width: 0%"></div>
        </div>
      </div>
      <div class="flex flex-col sm:flex-row gap-3">
        <button id="review-btn" type="button" class="w-full bg-slate-700 hover:bg-slate-600 text-slate-200 font-semibold py-3.5 px-4 rounded-xl text-sm">Soruları İncele</button>
        <button id="restart-btn" type="button" class="w-full bg-indigo-600 hover:bg-indigo-500 text-white font-bold py-3.5 px-4 rounded-xl text-sm shadow-lg shadow-indigo-600/30">Testi Yeniden Çöz</button>
      </div>
    </section>
  </main>

  <footer class="bg-slate-900 border-t border-slate-800 py-4 text-center text-xs text-slate-500">
    7. Sınıf Fen Bilgisi Interaktif Öğrenme Materyali · MEB müfredatına uygundur
  </footer>

  <script>
    const OPTION_LABELS = ["A", "B", "C", "D"];
    const KATEX_OPTIONS = {
      delimiters: [
        { left: "$$", right: "$$", display: true },
        { left: "$", right: "$", display: false }
      ],
      throwOnError: false
    };

    const questions = [
      {
        q: "1. Günlük hayatta yapılan bazı eylemler fiziksel anlamda iş olarak kabul edilirken bazıları edilmez. Buna göre, aşağıdakilerden hangisi fiziksel anlamda \"iş\" yapıldığına örnek gösterilebilir?",
        options: [
          "Sırt çantasıyla düz yolda yürüyen öğrenci",
          "Yerden eline aldığı bir kitabı yukarıdaki rafa yerleştiren öğrenci",
          "Duvarı itmeye çalışan ama hareket ettiremeyen çocuk",
          "Masa başında sabit oturarak ders çalışan öğrenci"
        ],
        correct: 1,
        explanation: "Fiziksel anlamda iş yapılabilmesi için cisme kuvvet uygulanmalı ve cisim kuvvet doğrultusunda yol almalıdır. Kitabı yukarı kaldırırken uygulanan düşey kuvvet ile kitabın aldığı yol aynı doğrultudadır."
      },
      {
        q: "2. Fiziksel anlamda yapılan işin büyüklüğü hangi faktörlere doğrudan bağlıdır?",
        options: [
          "Sadece uygulanan kuvvetin büyüklüğüne",
          "Sadece cismin aldığı yola",
          "Uygulanan kuvvetin büyüklüğü ve cismin bu kuvvet doğrultusunda aldığı yol",
          "Cismin kütlesine ve yüzeyin sürtünmesine"
        ],
        correct: 2,
        explanation: "Fiziksel anlamda iş $W = F \\cdot \\Delta x$ formülü ile ifade edilir. Yapılan iş, uygulanan kuvvetin büyüklüğüne ve cismin bu kuvvet doğrultusunda aldığı yola doğrudan bağlıdır."
      },
      {
        q: "3. Özdeş üç kutu, yatay sürtünmesiz düzlemde farklı kuvvetler yardımıyla farklı mesafelerde hareket ettiriliyor. Hangi seçenekte yapılan işin en fazla olması beklenir?",
        options: [
          "$10\\text{ N}$ kuvvetle $2\\text{ m}$ çekilen kutu",
          "$15\\text{ N}$ kuvvetle $2\\text{ m}$ çekilen kutu",
          "$10\\text{ N}$ kuvvetle $5\\text{ m}$ çekilen kutu",
          "$20\\text{ N}$ kuvvetle $4\\text{ m}$ çekilen kutu"
        ],
        correct: 3,
        explanation: "Yapılan iş kuvvet ile yolun çarpımına eşittir ($W = F \\cdot x$). D seçeneğinde $20\\text{ N} \\times 4\\text{ m} = 80\\text{ J}$ ile en büyük iş elde edilir."
      },
      {
        q: "4. Bir market arabasını yatay doğrultuda iterken, arabanın aldığı yol sabit tutulup uygulanan kuvvet iki katına çıkarılırsa fiziksel anlamda yapılan iş nasıl değişir?",
        options: ["Yarıya düşer", "Değişmez", "İki katına çıkar", "Dört katına çıkar"],
        correct: 2,
        explanation: "İş, uygulanan kuvvet ile doğru orantılıdır. Yol sabitken kuvvet 2 katına çıkarılırsa yapılan iş de doğrudan 2 katına çıkar."
      },
      {
        q: "5. Aşağıdaki durumların hangisinde fiziksel anlamda yapılan iş sıfırdır?",
        options: [
          "Bir sandığı yatay zeminde iterek ilerletmek",
          "Yatay yolda yürüyen birinin elinde tuttuğu çantayı yukarı kaldırmadan taşıması",
          "Merdivenlerden yukarı doğru tırmanan sporcu",
          "Taşı yerden kaldırıp masaya koymak"
        ],
        correct: 1,
        explanation: "Çantayı tutmak için yukarı doğru kuvvet uygulanır fakat hareket yatay doğrultudadır. Kuvvet ile hareket doğrultusu dik ($90^\\circ$) olduğu için fiziksel anlamda iş yapılmaz (iş sıfırdır)."
      },
      {
        q: "6. Hareket halindeki bir kamyonun sahip olduğu kinetik enerji; kamyonun sürati ve kütlesi dikkate alındığında hangisine bağlı olarak artar?",
        options: [
          "Sadece kütlesi arttıkça",
          "Sadece sürati azaldıkça",
          "Sürati ve kütlesi arttıkça kinetik enerji artar",
          "Kütlesi azalıp sürati azaldıkça"
        ],
        correct: 2,
        explanation: "Kinetik enerji cismin hem kütlesine hem de süratine bağlıdır. Cismin kütlesi ve sürati arttıkça sahip olduğu kinetik enerji de artar."
      },
      {
        q: "7. Aynı süratle hareket eden iki araçtan kütlesi daha büyük olan kamyon ile kütlesi küçük olan otomobil karşılaştırıldığında ne söylenebilir?",
        options: [
          "Otomobilin kinetik enerjisi daha büyüktür",
          "Kamyonun kinetik enerjisi otomobilinkinden daha fazladır",
          "Her ikisinin kinetik enerjisi eşittir",
          "Kütle kinetik enerjiyi etkilemez"
        ],
        correct: 1,
        explanation: "Süratleri eşit olan araçlardan kütlesi büyük olanın kinetik enerjisi daha fazladır. Bu nedenle kamyonun kinetik enerjisi otomobilinkinden büyüktür."
      },
      {
        q: "8. Esnek bir yayın sıkıştırılması veya gerilmesi sonucunda yayda depolanan enerji türü aşağıdakilerden hangisidir?",
        options: ["Çekim potansiyel enerjisi", "Kinetik enerji", "Esneklik potansiyel enerjisi", "Isı enerjisi"],
        correct: 2,
        explanation: "Yay, sünger, paket lastiği gibi esnek maddelerin sıkıştırılması veya gerilmesi sonucu depolanan enerjiye esneklik potansiyel enerjisi denir."
      },
      {
        q: "9. Duvarda asılı duran özdeş iki tablodan biri birinci katta, diğeri dördüncü katta yerden aynı yükseklikte asılıdır. Yerden yükseklikleri eşit olan bu tablolardan dördüncü kattakinin yere göre potansiyel enerjisi için ne söylenebilir?",
        options: [
          "Dördüncü kattaki tablonun potansiyel enerjisi daha büyüktür",
          "Birinci kattaki tablonun potansiyel enerjisi daha büyüktür",
          "Yerden yükseklikleri ve kütleleri eşit olduğu için potansiyel enerjileri eşittir",
          "Tabloların potansiyel enerjisi yoktur"
        ],
        correct: 2,
        explanation: "Çekim potansiyel enerjisi cismin kütlesine ve yerden yüksekliğine bağlıdır. Özdeş tabloların yerden yükseklikleri eşit olduğu için çekim potansiyel enerjileri de eşittir."
      },
      {
        q: "10. Aşağıdaki olayların hangisinde çekim potansiyel enerjisinin kinetik enerjiye dönüştüğü gözlemlenir?",
        options: [
          "Daldan koparak yere doğru düşen bir elma",
          "Yerden yukarıya doğru fırlatılan bir taş",
          "Gerilmiş bir yaydan fırlayan ok",
          "Düz yolda sabit hızla giden bir araba"
        ],
        correct: 0,
        explanation: "Daldan düşen elma irtifa kaybettikçe çekim potansiyel enerjisi azalır, hızı arttığı için bu enerji kinetik enerjiye dönüşür."
      },
      {
        q: "11. Sürtünmesiz bir ortamda yukarı doğru düşey olarak atılan bir topun hareketi sırasında enerji değişimleri nasıl gerçekleşir?",
        options: [
          "Kinetik enerji artar, potansiyel enerji azalır",
          "Kinetik enerji azalırken çekim potansiyel enerji artar",
          "Hem kinetik hem potansiyel enerji artar",
          "Enerji değişimi gerçekleşmez"
        ],
        correct: 1,
        explanation: "Yukarı doğru fırlatılan top yükseldikçe yavaşlar (kinetik enerjisi azalır), yüksekliği arttığı için çekim potansiyel enerjisi artar."
      },
      {
        q: "12. Lunaparkta hareket eden bir trenin (hız treninin) en tepeden aşağıya doğru hızlanarak kaydığı esnada enerjideki değişimlerle ilgili aşağıdakilerden hangisi doğrudur?",
        options: [
          "Potansiyel enerji artar, kinetik enerji azalır",
          "Potansiyel enerji azalır, kinetik enerji artar",
          "Her iki enerji türü de azalır",
          "Her iki enerji türü de sabittir"
        ],
        correct: 1,
        explanation: "Tren aşağı inerken yüksekliği azaldığı için çekim potansiyel enerjisi azalır, hızı arttığı için kinetik enerjisi artar."
      },
      {
        q: "13. Sürtünmeli bir yüzeyde kayarak yavaşlayan bir kutunun mekanik enerjisindeki değişim için tümevarımsal bir akıl yürütmeyle hangi sonuca varılır?",
        options: [
          "Mekanik enerji tamamen yok olur",
          "Mekanik enerji artar",
          "Mekanik enerji sürtünmeden dolayı ısı enerjisine dönüşerek azalır, ancak toplam enerji korunur",
          "Mekanik enerji değişmez"
        ],
        correct: 2,
        explanation: "Sürtünmeli ortamlarda mekanik enerji (kinetik + potansiyel) sürtünme kuvveti nedeniyle ısı enerjisine dönüşür. Mekanik enerji azalsa da evrendeki toplam enerji korunur."
      },
      {
        q: "14. Bir öğrenci, havaya attığı topun tepe noktasına ulaştığı anı ve yere çarpma anını gözlemliyor. Bu gözlemlere dayanarak enerjinin korunumu ilkesine varan öğrenci, tümevarımsal olarak aşağıdakilerden hangisini söyleyemez?",
        options: [
          "Tepe noktasında potansiyel enerji maksimumdur",
          "Yere çarpma anında kinetik enerji maksimumdur",
          "Topun en tepe noktada sadece kinetik enerjisi vardır",
          "Toplam enerji hareket boyunca sabittir"
        ],
        correct: 2,
        explanation: "Top en tepe noktaya ulaştığında bir anlığına durur ($v=0$). Bu nedenle kinetik enerjisi sıfır, potansiyel enerjisi maksimumdur."
      },
      {
        q: "15. Aşağıdaki durumların hangisinde hem kinetik enerji hem de çekim potansiyel enerji aynı anda bulunur?",
        options: [
          "Masa üzerinde duran bir kitap",
          "Gökyüzünde belli bir yükseklikte uçmakta olan bir kuş",
          "Yatay yolda duran araba",
          "Sıkıştırılmış yay"
        ],
        correct: 1,
        explanation: "Belli bir yükseklikte uçan kuşun hem yerden yüksekliğinden dolayı çekim potansiyel enerjisi hem de hareketinden dolayı kinetik enerjisi vardır."
      },
      {
        q: "16. Özdeş üç kamyon sırasıyla $60\\text{ km/h}$, $80\\text{ km/h}$ ve $100\\text{ km/h}$ süratlerle hareket etmektedir. Bu kamyonların kinetik enerjileri arasındaki ilişki nasıldır?",
        options: [
          "$60\\text{ km/h}$ süratle gidenin kinetik enerjisi en büyüktür",
          "$80\\text{ km/h}$ süratle gidenin kinetik enerjisi en büyüktür",
          "$100\\text{ km/h}$ süratle gidenin kinetik enerjisi en büyüktür",
          "Hepsinin kinetik enerjisi eşittir"
        ],
        correct: 2,
        explanation: "Kütleleri özdeş olan araçlardan sürati en yüksek olan $100\\text{ km/h}$ süratli kamyonun kinetik enerjisi en büyüktür."
      },
      {
        q: "17. Fiziksel anlamda iş yapabilmek için gerekli şartları inceleyen bir öğrenci, aşağıdaki işlemlerden hangisinde iş yapıldığını matematiksel veya mantıksal olarak kanıtlayamaz?",
        options: [
          "Masayı $2\\text{ m}$ ileri itmek",
          "Sırt çantasını yerden kaldırıp sırtına takmak",
          "Ağır bir dolabı yerinden oynatamadan saatlerce itmek",
          "Merdivenlerden bir koli taşımak"
        ],
        correct: 2,
        explanation: "Dolap itilip hareket ettirilemediğinde alınan yol $\\Delta x = 0$ olur. $W = F \\cdot 0 = 0$ olduğu için fiziksel anlamda iş yapılmamış olur."
      },
      {
        q: "18. Aşağıdaki durumlardan hangisinde çekim potansiyel enerjisi diğerlerinden farklı bir etkene bağlı olarak değişir?",
        options: [
          "Kütlesi büyük olan cismin yüksekliği",
          "Yüksekliği fazla olan aynı kütleli cisim",
          "Esnek yayın gerilme miktarı",
          "Dağın tepesindeki kaya parçası"
        ],
        correct: 2,
        explanation: "A, B ve D seçenekleri yerçekimi kuvvetine bağlı çekim potansiyel enerjisi ile ilgilidir. C seçeneği ise yayın esneklik özelliğine bağlı esneklik potansiyel enerjisidir."
      },
      {
        q: "19. Sürtünmesiz bir ray üzerinde hareket eden bir bilyenin tepe noktalarındaki ve çukurdaki durumları inceleniyor. Bilyenin potansiyel enerjisinin en fazla olduğu nokta için ne söylenebilir?",
        options: [
          "En alt çukur noktada potansiyel enerji en fazladır",
          "Yerden yüksekliğinin en fazla olduğu noktada potansiyel enerji en fazladır",
          "Hızının en yüksek olduğu noktada potansiyel enerji en fazladır",
          "Her noktada potansiyel enerji eşittir"
        ],
        correct: 1,
        explanation: "Çekim potansiyel enerjisi yükseklikle doğru orantılıdır. Yerden yüksekliğin en fazla olduğu tepe noktasında potansiyel enerji maksimumdur."
      },
      {
        q: "20. Bir okçu yayı gerdiğinde yayda enerji depolanır. Okçu oku serbest bıraktığında bu enerjide nasıl bir dönüşüm gözlenir?",
        options: [
          "Kinetik enerji potansiyel enerjiye dönüşür",
          "Esneklik potansiyel enerjisi okun kinetik enerjisine dönüşür",
          "Çekim potansiyel enerjisi ısı enerjisine dönüşür",
          "Isı enerjisi kinetik enerjiye dönüşür"
        ],
        correct: 1,
        explanation: "Gerilen yayda depolanan esneklik potansiyel enerjisi, serbest bırakıldığında oku ileri doğru fırlatarak kinetik enerjiye dönüşür."
      },
      {
        q: "21. Özdeş kütleli iki arabadan biri $20\\text{ m/s}$ diğeri $10\\text{ m/s}$ süratle hareket etmektedir. Bu araçların kinetik enerjilerini karşılaştıran bir öğrenci hangi bilimsel çıkarımda bulunmalıdır?",
        options: [
          "Sürati az olanın kinetik enerjisi büyüktür",
          "Sürati fazla olan aracın kinetik enerjisi diğerininkinden büyüktür",
          "İki aracın da kinetik enerjisi eşittir",
          "Sürat kinetik enerjiyi etkilemez"
        ],
        correct: 1,
        explanation: "Kütleleri eşit olduğunda, sürati fazla olan ($20\\text{ m/s}$) aracın kinetik enerjisi sürati az olan ($10\\text{ m/s}$) araçtan daha büyüktür."
      },
      {
        q: "22. Fiziksel anlamda iş kavramıyla ilgili aşağıda verilen tablodaki bilgilerden hangisi yanlıştır?",
        options: [
          "İş birimi Joule'dür",
          "Kuvvet ve alınan yol doğrultuları aynı olmalıdır",
          "Cisme uygulanan kuvvet sıfırdan farklıysa, yer değiştirme olmasa bile kesinlikle iş yapılır",
          "Kuvvet arttıkça yapılan iş artar"
        ],
        correct: 2,
        explanation: "Kuvvet sıfırdan farklı olsa bile cisim yer değiştirmiyorsa (yol almıyorsa) fiziksel anlamda iş yapılmaz."
      },
      {
        q: "23. Serbest bırakılan bir topun yere düşerken potansiyel ve kinetik enerjilerindeki değişimi tümevarımsal bir yaklaşımla ele alan bir öğrenci hangi sonuca varır?",
        options: [
          "Top düştükçe toplam enerji sürekli artar",
          "Potansiyel enerji azaldıkça kinetik enerji artar ve toplam mekanik enerji korunur",
          "Topun hem kinetik hem potansiyel enerjisi sürekli azalır",
          "Yere düşerken enerji tamamen kaybolur"
        ],
        correct: 1,
        explanation: "Top yere düşerken yükseklik azaldığı için potansiyel enerji azalır, sürat arttığı için kinetik enerji artar. Sürtünmesiz ortamda toplam mekanik enerji korunur."
      },
      {
        q: "24. Aşağıdaki durumlardan hangisi, fiziksel anlamda iş yapılmasına örnek olarak gösterilebilir?",
        options: [
          "Eldeki çantayı sallamadan düz yolda taşımak",
          "Bir haltercinin ağır halterleri yerden kaldırarak başının üzerine kadar çıkarması",
          "Sırt çantasıyla otobüs beklemek",
          "Kutuya bastırıp hareket ettirmemek"
        ],
        correct: 1,
        explanation: "Halteri yerden kaldırırken uygulanan kuvvet yukarı yönlüdür ve halter de yukarı doğru yol alır. Doğrultular aynı olduğu için fiziksel anlamda iş yapılır."
      },
      {
        q: "25. Farklı yüksekliklerde bulunan özdeş kütleli saksılardan hangisinin yere göre çekim potansiyel enerjisi en fazladır?",
        options: [
          "Zemin katta bulunan saksı",
          "1. kattaki balkonda bulunan saksı",
          "2. kattaki balkonda bulunan saksı",
          "En üst kattaki balkonda bulunan saksı"
        ],
        correct: 3,
        explanation: "Özdeş kütleli cisimlerden yerden yüksekliği en fazla olanın çekim potansiyel enerjisi en büyüktür. Bu nedenle en üst kattaki saksının enerjisi en fazladır."
      },
      {
        q: "26. Sürtünmesiz bir ray üzerinde serbest bırakılan bir arabanın hareketi incelendiğinde, enerjinin korunduğu sonucuna ulaşılmaktadır. Bu durum hangi tümevarımsal akıl yürütmeyi destekler?",
        options: [
          "Kinetik enerji her zaman artar",
          "Sistemdeki kinetik ve potansiyel enerjilerin toplamı her noktada sabittir",
          "Potansiyel enerji asla tükenmez",
          "Sürtünmesiz sistemlerde enerji kaybolur"
        ],
        correct: 1,
        explanation: "Sürtünmesiz sistemlerde toplam mekanik enerji (kinetik enerji + potansiyel enerji) sabittir ve korunur."
      },
      {
        q: "27. Kinetik enerji ve potansiyel enerjinin ortak özellikleriyle ilgili olarak aşağıdakilerden hangisi söylenebilir?",
        options: [
          "İkisi de sadece cismin hızına bağlıdır",
          "İkisi de enerji çeşitleridir ve birimleri Joule'dür",
          "İkisi de sadece cismin yüksekliğine bağlıdır",
          "Her ikisi de sadece esnek maddelerde bulunur"
        ],
        correct: 1,
        explanation: "Kinetik ve potansiyel enerjinin her ikisi de temel mekanik enerji türleridir ve SI birim sisteminde birimleri Joule (J)'dür."
      },
      {
        q: "28. Yatay ve sürtünmesiz bir yolda durmakta olan cisme uygulanan yatay kuvvetin yola bağlı değişim grafiği verilmiştir. Yapılan işin miktarını artırmak için ne yapılmalıdır?",
        options: [
          "Uygulanan kuvveti veya cismin aldığı yolu artırmak",
          "Sadece kütleyi artırmak",
          "Alınan yolu azaltmak",
          "Uygulanan kuvveti azaltmak"
        ],
        correct: 0,
        explanation: "İş $W = F \\cdot x$ formülüne bağlı olduğundan yapılan işi artırmak için uygulanan kuvvet ($F$) veya alınan yol ($x$) artırılmalıdır."
      },
      {
        q: "29. Aşağıdaki olayların hangisinde enerji dönüşümü sırasında enerjinin korunduğu kuralı bozulmuş gibi görünse de aslında enerji ısı veya ses enerjisine dönüşerek korunmaya devam eder?",
        options: [
          "Uzay boşluğunda ilerleyen bir roket",
          "Yere düşen bir topun bir süre sonra zıplamayı bırakıp durması",
          "Sürtünmesiz ortamda salınan sarkaç",
          "Güneş enerjisinin elektrik enerjisine dönüşmesi"
        ],
        correct: 1,
        explanation: "Top zıplarken zemin ve hava ile sürtünür, her zıplayışta mekanik enerjisinin bir kısmı ısı ve ses enerjisine dönüşür. Mekanik enerji azalsa da toplam enerji tamamen korunur."
      },
      {
        q: "30. Fiziksel anlamda iş, kinetik enerji, potansiyel enerji ve enerjinin korunumu konularını kapsayan bir çalışma yapan öğrenci şu sonuca varıyor: \"Kuvvet uygulanan cisim yol alıyorsa iş yapılır; bu iş cisme enerji olarak aktarılır ve enerji tür değiştirse de toplam miktar her zaman korunur.\" Bu öğrencinin ulaştığı yargı neyi ifade eder?",
        options: [
          "İş yapılabilmesi için sadece kütlenin önemli olduğunu",
          "Enerjinin zamanla kendiliğinden yok olduğunu",
          "Fiziksel olaylar arasındaki temel enerji ilişkisini ve tümevarımsal genel prensibi",
          "Sürtünmenin enerjiyi çoğalttığını"
        ],
        correct: 2,
        explanation: "Öğrenci, gözlemlediği özel durumlardan hareketle iş, enerji aktarımı ve korunan genel enerji prensibine ulaşarak tümevarımsal bilimsel bir çıkarım yapmıştır."
      }
    ];

    const el = {
      welcome: document.getElementById("welcome-screen"),
      quiz: document.getElementById("quiz-screen"),
      result: document.getElementById("result-screen"),
      stats: document.getElementById("stats-header"),
      grid: document.getElementById("question-grid"),
      question: document.getElementById("question-text"),
      options: document.getElementById("options-container"),
      feedback: document.getElementById("feedback-banner"),
      status: document.getElementById("answered-status"),
      progress: document.getElementById("progress-bar"),
      currentNum: document.getElementById("current-q-num"),
      prev: document.getElementById("prev-btn"),
      next: document.getElementById("next-btn"),
      correctBadge: document.getElementById("score-correct-badge"),
      wrongBadge: document.getElementById("score-wrong-badge"),
      scoreCorrect: document.getElementById("score-correct"),
      scoreWrong: document.getElementById("score-wrong"),
      scoreEmpty: document.getElementById("score-empty"),
      accuracyText: document.getElementById("accuracy-percentage"),
      accuracyBar: document.getElementById("accuracy-bar"),
      resultIcon: document.getElementById("result-icon"),
      resultText: document.getElementById("result-feedback-text")
    };

    const state = {
      index: 0,
      answers: Array(questions.length).fill(null)
    };

    function showScreen(name) {
      el.welcome.classList.toggle("hidden", name !== "welcome");
      el.quiz.classList.toggle("hidden", name !== "quiz");
      el.quiz.classList.toggle("flex", name === "quiz");
      el.result.classList.toggle("hidden", name !== "result");
      el.stats.classList.toggle("hidden", name === "welcome");
      el.stats.classList.toggle("flex", name !== "welcome");
    }

    function renderMath(node) {
      if (window.renderMathInElement && node) {
        renderMathInElement(node, KATEX_OPTIONS);
      }
    }

    function tally() {
      let correct = 0;
      let wrong = 0;
      let empty = 0;
      state.answers.forEach((ans, i) => {
        if (ans === null) empty += 1;
        else if (ans === questions[i].correct) correct += 1;
        else wrong += 1;
      });
      return { correct, wrong, empty };
    }

    function dotClass(idx) {
      const base = "w-7 h-7 rounded-lg text-xs font-semibold flex items-center justify-center transition";
      if (idx === state.index) return `${base} ring-2 ring-indigo-400 bg-indigo-600 text-white`;
      if (state.answers[idx] === null) return `${base} bg-slate-800 text-slate-400 hover:bg-slate-700`;
      if (state.answers[idx] === questions[idx].correct) {
        return `${base} bg-emerald-500/20 text-emerald-400 border border-emerald-500/40`;
      }
      return `${base} bg-rose-500/20 text-rose-400 border border-rose-500/40`;
    }

    function renderGrid() {
      el.grid.replaceChildren();
      questions.forEach((_, idx) => {
        const btn = document.createElement("button");
        btn.type = "button";
        btn.textContent = String(idx + 1);
        btn.className = dotClass(idx);
        btn.setAttribute("aria-label", `Soru ${idx + 1}`);
        btn.addEventListener("click", () => showQuestion(idx));
        el.grid.appendChild(btn);
      });
    }

    function optionClass(answered, optIndex, qData, selected) {
      const base = "w-full text-left p-4 rounded-2xl border transition duration-200 flex items-start justify-between gap-3";
      if (!answered) {
        return `${base} bg-slate-900/60 border-slate-700/80 hover:border-indigo-500 hover:bg-indigo-500/10 text-slate-200`;
      }
      if (optIndex === qData.correct) {
        return `${base} bg-emerald-500/20 border-emerald-500 text-emerald-200 font-medium`;
      }
      if (selected === optIndex) {
        return `${base} bg-rose-500/20 border-rose-500 text-rose-200 font-medium`;
      }
      return `${base} bg-slate-900/40 border-slate-800 text-slate-500 opacity-50`;
    }

    function showQuestion(index) {
      state.index = index;
      const qData = questions[index];
      const selected = state.answers[index];
      const answered = selected !== null;
      const total = questions.length;

      el.currentNum.textContent = String(index + 1);
      el.question.innerHTML = qData.q;
      el.progress.style.width = `${((index + 1) / total) * 100}%`;
      el.progress.parentElement.setAttribute("aria-valuenow", String(index + 1));
      el.status.innerHTML = answered
        ? '<span class="text-emerald-400">✓ Cevaplandı</span>'
        : '<span class="text-slate-400">Cevaplanmadı</span>';

      el.options.replaceChildren();
      qData.options.forEach((opt, optIndex) => {
        const btn = document.createElement("button");
        btn.type = "button";
        btn.disabled = answered;
        btn.className = optionClass(answered, optIndex, qData, selected);
        btn.setAttribute("aria-pressed", String(selected === optIndex));

        const icon = answered && optIndex === qData.correct
          ? '<span class="pointer-events-none w-6 h-6 rounded-full bg-emerald-500/30 text-emerald-400 border border-emerald-500 flex items-center justify-center text-xs font-bold">✓</span>'
          : answered && selected === optIndex
            ? '<span class="pointer-events-none w-6 h-6 rounded-full bg-rose-500/30 text-rose-400 border border-rose-500 flex items-center justify-center text-xs font-bold">✕</span>'
            : "";

        btn.innerHTML = `
          <div class="flex items-start gap-3 pointer-events-none">
            <span class="w-7 h-7 rounded-xl bg-slate-800 text-slate-300 text-xs font-bold flex items-center justify-center flex-shrink-0 mt-0.5 border border-slate-700">${OPTION_LABELS[optIndex]}</span>
            <span class="text-sm md:text-base leading-snug">${opt}</span>
          </div>
          ${icon}
        `;
        btn.addEventListener("click", () => selectAnswer(optIndex));
        el.options.appendChild(btn);
      });

      if (answered) {
        const isCorrect = selected === qData.correct;
        el.feedback.classList.remove("hidden");
        if (isCorrect) {
          el.feedback.className = "p-4 rounded-2xl border mb-6 bg-emerald-500/10 border-emerald-500/40 text-emerald-300 text-sm leading-relaxed";
          el.feedback.innerHTML = `
            <div class="font-bold flex items-center gap-2 text-emerald-400 mb-1"><span>🎉</span> Tebrikler! Doğru cevap.</div>
            <div>${qData.explanation}</div>
          `;
        } else {
          el.feedback.className = "p-4 rounded-2xl border mb-6 bg-rose-500/10 border-rose-500/40 text-rose-300 text-sm leading-relaxed";
          el.feedback.innerHTML = `
            <div class="font-bold flex items-center gap-2 text-rose-400 mb-1"><span>❌</span> Yanlış cevap.</div>
            <div class="mb-1 text-slate-200 font-medium">Doğru şık: <strong>${OPTION_LABELS[qData.correct]}</strong></div>
            <div class="text-xs text-rose-200/90">${qData.explanation}</div>
          `;
        }
      } else {
        el.feedback.classList.add("hidden");
        el.feedback.replaceChildren();
      }

      renderMath(el.question);
      renderMath(el.options);
      if (answered) renderMath(el.feedback);

      [...el.grid.children].forEach((dot, i) => {
        dot.className = dotClass(i);
      });

      const { correct, wrong } = tally();
      el.correctBadge.textContent = String(correct);
      el.wrongBadge.textContent = String(wrong);

      el.prev.disabled = index === 0;
      const last = index === total - 1;
      el.next.textContent = last ? "Testi Bitir 🏁" : "Sonraki →";
      el.next.className = last
        ? "bg-emerald-600 hover:bg-emerald-500 text-white px-6 py-2.5 rounded-xl font-bold text-sm shadow-lg shadow-emerald-600/30"
        : "bg-indigo-600 hover:bg-indigo-500 text-white px-6 py-2.5 rounded-xl font-semibold text-sm shadow-lg shadow-indigo-600/30";
    }

    function selectAnswer(optIndex) {
      if (state.answers[state.index] !== null) return;
      state.answers[state.index] = optIndex;
      showQuestion(state.index);
    }

    function startQuiz() {
      showScreen("quiz");
      renderGrid();
      showQuestion(0);
    }

    function restartQuiz() {
      state.answers = Array(questions.length).fill(null);
      state.index = 0;
      startQuiz();
    }

    function finishQuiz() {
      const { correct, wrong, empty } = tally();
      const accuracy = Math.round((correct / questions.length) * 100);

      el.scoreCorrect.textContent = String(correct);
      el.scoreWrong.textContent = String(wrong);
      el.scoreEmpty.textContent = String(empty);
      el.accuracyText.textContent = `${accuracy}%`;
      el.accuracyBar.style.width = `${accuracy}%`;

      if (accuracy >= 85) {
        el.resultIcon.textContent = "🏆";
        el.resultText.textContent = "Mükemmel! Ünite konularına tam olarak hakimsiniz.";
      } else if (accuracy >= 60) {
        el.resultIcon.textContent = "⭐";
        el.resultText.textContent = "Tebrikler! Güzel bir başarı, eksik konularınızı inceleyebilirsiniz.";
      } else {
        el.resultIcon.textContent = "📚";
        el.resultText.textContent = "Konuları tekrar gözden geçirerek başarı oranınızı artırabilirsiniz.";
      }

      if (empty > 0) {
        el.resultText.textContent += ` ${empty} soru boş bırakıldı.`;
      }

      showScreen("result");
    }

    function nextQuestion() {
      if (state.index < questions.length - 1) showQuestion(state.index + 1);
      else finishQuiz();
    }

    function prevQuestion() {
      if (state.index > 0) showQuestion(state.index - 1);
    }

    document.getElementById("start-btn").addEventListener("click", startQuiz);
    document.getElementById("review-btn").addEventListener("click", () => {
      showScreen("quiz");
      renderGrid();
      showQuestion(0);
    });
    document.getElementById("restart-btn").addEventListener("click", restartQuiz);
    el.prev.addEventListener("click", prevQuestion);
    el.next.addEventListener("click", nextQuestion);

    document.addEventListener("keydown", (e) => {
      if (el.quiz.classList.contains("hidden")) return;
      if (e.key === "ArrowLeft") prevQuestion();
      else if (e.key === "ArrowRight") nextQuestion();
      else {
        const map = { a: 0, b: 1, c: 2, d: 3, A: 0, B: 1, C: 2, D: 3 };
        if (map[e.key] !== undefined) selectAnswer(map[e.key]);
      }
    });
  </script>
</body>
</html>
