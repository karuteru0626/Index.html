<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="theme-color" content="#102542">
  <title>TOEIC TRAINER | 10問試作版</title>
  <style>
    :root {
      font-family: -apple-system, BlinkMacSystemFont,
        "Hiragino Kaku Gothic ProN", "Yu Gothic", sans-serif;
      color: #17263c;
      background: #f3f6fb;
      font-synthesis: none;
    }
    * { box-sizing: border-box; }
    body { margin: 0; }
    button { font: inherit; cursor: pointer; }
    button:focus-visible {
      outline: 3px solid #ffb933;
      outline-offset: 3px;
    }
    .shell {
      max-width: 760px;
      margin: auto;
      padding: 20px 16px 70px;
    }
    .top {
      background: #102542;
      color: white;
      padding: 34px 25px;
      border-radius: 25px;
      margin-bottom: 20px;
      box-shadow: 0 15px 35px #10254220;
    }
    .eyebrow {
      color: #a8e3e4;
      font-size: .75rem;
      font-weight: 800;
      letter-spacing: .17em;
      margin: 0 0 8px;
    }
    .top h1 {
      font-size: clamp(1.6rem, 5vw, 2.4rem);
      letter-spacing: .03em;
      margin: 0;
    }
    .top p:last-child {
      color: #c8d6e8;
      margin: 9px 0 0;
      line-height: 1.6;
      font-size: .92rem;
    }
    .panel {
      background: white;
      border: 1px solid #e3e9f2;
      border-radius: 22px;
      padding: 24px;
      box-shadow: 0 8px 28px #12304a0b;
      margin-bottom: 16px;
    }
    .panel h2 {
      font-size: 1.22rem;
      margin: 0 0 12px;
    }
    .muted { color: #627188; }
    .small { font-size: .86rem; }
    .intro {
      line-height: 1.75;
      margin: 0 0 20px;
    }
    .stats {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 10px;
      margin-bottom: 22px;
    }
    .stat {
      background: #f0f5fa;
      border-radius: 15px;
      padding: 13px 10px;
      text-align: center;
    }
    .stat strong {
      display: block;
      font-size: 1.45rem;
      color: #103a62;
    }
    .stat span {
      font-size: .75rem;
      color: #52627a;
    }
    .filters {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
      margin: 11px 0 16px;
    }
    .chip {
      border: 1px solid #cdd9e7;
      border-radius: 999px;
      background: white;
      color: #294260;
      padding: 9px 13px;
      font-size: .86rem;
      font-weight: 700;
    }
    .chip[aria-pressed=true] {
      background: #124f71;
      color: white;
      border-color: #124f71;
    }
    .primary, .secondary {
      border-radius: 13px;
      padding: 12px 18px;
      font-weight: 800;
      min-height: 48px;
    }
    .primary {
      background: #0f6475;
      color: white;
      border: 1px solid #0f6475;
    }
    .primary:hover { background: #0b5262; }
    .primary:disabled {
      opacity: .45;
      cursor: not-allowed;
    }
    .secondary {
      background: #fff;
      color: #15566a;
      border: 1px solid #b8cdd7;
    }
    .secondary:hover { background: #edf6f8; }
    .row {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      flex-wrap: wrap;
    }
    .badge {
      display: inline-block;
      background: #e9f4f5;
      color: #0e6671;
      font-size: .78rem;
      font-weight: 800;
      border-radius: 999px;
      padding: 6px 10px;
    }
    .badge.advanced {
      background: #f4eafb;
      color: #773995;
    }
    .badge.basic {
      background: #e9f2fd;
      color: #315d9d;
    }
    .progress {
      height: 8px;
      border-radius: 99px;
      background: #e9eef5;
      overflow: hidden;
      margin: 17px 0 23px;
    }
    .progress > span {
      display: block;
      height: 100%;
      background: #20a3a2;
      border-radius: 99px;
      transition: width .2s;
    }
    .question {
      font-family: Georgia, "Times New Roman", serif;
      font-size: clamp(1.2rem, 4.3vw, 1.58rem);
      line-height: 1.55;
      margin: 20px 0 23px;
      white-space: pre-line;
      color: #15243b;
    }
    .choices {
      display: grid;
      gap: 10px;
    }
    .choice {
      width: 100%;
      text-align: left;
      border: 1px solid #cbd8e6;
      border-radius: 14px;
      background: #fff;
      padding: 15px 16px;
      line-height: 1.45;
      display: flex;
      gap: 14px;
      align-items: baseline;
      color: #17263c;
    }
    .choice:hover:not(:disabled) {
      border-color: #0b7886;
      background: #f0fafa;
    }
    .choice:disabled { cursor: default; }
    .choice b {
      color: #176777;
      min-width: 20px;
    }
    .choice.correct {
      border-color: #128361;
      background: #eaf8f2;
    }
    .choice.wrong {
      border-color: #cc5858;
      background: #fff0ef;
    }
    .choice.correct b { color: #128361; }
    .choice.wrong b { color: #bd3c3c; }
    .feedback {
      margin-top: 24px;
      border-top: 1px solid #e2eaf0;
      padding-top: 22px;
    }
    .verdict {
      font-weight: 850;
      font-size: 1.16rem;
      margin-bottom: 7px;
    }
    .verdict.yes { color: #087759; }
    .verdict.no { color: #ae4141; }
    .answer {
      font-weight: 700;
      margin: 0 0 18px;
    }
    .block {
      border-left: 3px solid #1d8790;
      padding: 1px 0 1px 13px;
      margin: 19px 0;
    }
    .block h3, .feedback h3 {
      font-size: .97rem;
      margin: 0 0 8px;
      color: #163b55;
    }
    .block p {
      margin: 0;
      white-space: pre-line;
      line-height: 1.75;
    }
    .explain-list {
      padding: 0;
      list-style: none;
      display: grid;
      gap: 8px;
      margin: 9px 0 20px;
    }
    .explain-list li {
      background: #f3f7fa;
      padding: 11px 12px;
      border-radius: 10px;
      line-height: 1.6;
    }
    .vocab {
      margin: 0 0 20px;
      padding-left: 20px;
      line-height: 1.75;
    }
    .copybox {
      white-space: pre-wrap;
      background: #f4f6fa;
      border-radius: 12px;
      padding: 14px;
      font-size: .87rem;
      line-height: 1.65;
      margin: 9px 0 12px;
    }
    .actions {
      display: flex;
      gap: 9px;
      flex-wrap: wrap;
      margin-top: 23px;
    }
    .actions .primary { flex: 1; }
    .result-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 8px;
      margin: 20px 0;
    }
    .result-grid div {
      background: #f2f6fa;
      border-radius: 12px;
      text-align: center;
      padding: 13px 8px;
      font-size: .84rem;
    }
    .result-grid b {
      display: block;
      font-size: 1.22rem;
      color: #14546c;
      margin: 5px;
    }
    .footer {
      text-align: center;
      color: #758399;
      font-size: .78rem;
      padding: 4px 0 20px;
    }
    #live {
      position: absolute;
      width: 1px;
      height: 1px;
      overflow: hidden;
      clip: rect(0, 0, 0, 0);
    }
    @media (max-width: 480px) {
      .panel { padding: 19px; }
      .top { padding: 26px 20px; }
      .stats { gap: 5px; }
      .stat { padding: 12px 3px; }
      .result-grid { gap: 5px; }
      .actions button { width: 100%; }
    }
  </style>
</head>
<body>
  <div class="shell">
    <header class="top">
      <p class="eyebrow">PERSONAL PRACTICE · PART 5</p>
      <h1>TOEIC TRAINER</h1>
      <p>一問ずつ解いて、文の構造まで理解する。</p>
    </header>
    <main id="app"></main>
    <p class="footer">
      10問試作版 · 学習記録はこのブラウザ内に保存されます
    </p>
  </div>
  <div id="live" role="status" aria-live="polite"></div>
  <script>
    "use strict";
    // 問題を追加するときは、同じ形式でここに追加してください。
    // idは重複させないでください。
    const QUESTIONS = [
      {
        id: "b01",
        level: "basic",
        topic: "動詞の形",
        question:
          "The finance department will _____ the invoices by Friday.",
        choices: [
          "processed",
          "process",
          "processing",
          "processes"
        ],
        answer: 1,
        structure:
          "S: The finance department\n" +
          "V: will process\n" +
          "O: the invoices\n" +
          "M: by Friday",
        reason:
          "助動詞 will の直後は動詞の原形。" +
          "process は「処理する」という他動詞で、" +
          "the invoices が目的語です。",
        options: [
          "A processed：過去形・過去分詞。will の直後には置けない。",
          "B process：動詞の原形。正解。",
          "C processing：現在分詞・動名詞。will の直後には置けない。",
          "D processes：三人称単数現在形・名詞の複数形。ここでは使えない。"
        ],
        vocab: [
          "invoice（名詞）：請求書",
          "process（他動詞）：～を処理する",
          "by Friday：金曜日までに（期限）"
        ],
        summary:
          "will＋動詞の原形 → process（処理する）。" +
          "process the invoices＝請求書を処理する。" +
          "by Friday＝金曜日までに。"
      },
      {
        id: "b02",
        level: "basic",
        topic: "前置詞",
        question:
          "Please send the completed form _____ the HR office.",
        choices: ["at", "to", "by", "from"],
        answer: 1,
        structure:
          "S: (You)［命令文なので省略］\n" +
          "V: send\n" +
          "O: the completed form\n" +
          "M: to the HR office",
        reason:
          "送付先を示す形は send A to B「AをBへ送る」。" +
          "ここで the HR office は送付先です。",
        options: [
          "A at：～で・～に。send A at B という送付先の形にはしない。",
          "B to：～へ。送付先を示すので正解。",
          "C by：～までに・～によって。送付先を示せない。",
          "D from：～から。送付元の意味になり、文脈に合わない。"
        ],
        vocab: [
          "completed（形容詞的な過去分詞）：記入済みの",
          "form（名詞）：用紙、書類",
          "HR office：人事部",
          "send A to B：AをBに送る"
        ],
        summary:
          "send A to B＝AをBへ送る。" +
          "the completed form＝記入済みの書類。" +
          "HR office＝人事部。"
      },
      {
        id: "b03",
        level: "basic",
        topic: "品詞",
        question:
          "The new software has significantly improved employee _____.",
        choices: [
          "productive",
          "productivity",
          "productively",
          "produce"
        ],
        answer: 1,
        structure:
          "S: The new software\n" +
          "V: has improved\n" +
          "O: employee productivity\n" +
          "M: significantly",
        reason:
          "improved の後には目的語となる名詞が必要です。" +
          "employee が前から名詞 productivity を修飾し、" +
          "「従業員の生産性」となります。",
        options: [
          "A productive：形容詞「生産的な」。この位置で目的語の中心にはなれない。",
          "B productivity：名詞「生産性」。正解。",
          "C productively：副詞「生産的に」。目的語になれない。",
          "D produce：動詞「生産する」／名詞「農産物」。意味が合わない。"
        ],
        vocab: [
          "productivity（名詞）：生産性",
          "productive（形容詞）：生産的な",
          "improve（他動詞・自動詞）：～を改善する／改善する",
          "significantly（副詞）：大幅に"
        ],
        summary:
          "improve＋目的語（名詞）。" +
          "employee productivity＝従業員の生産性。" +
          "significantly improve＝大幅に改善する。"
      },
      {
        id: "b04",
        level: "basic",
        topic: "動詞の語法",
        question:
          "Ms. Ito asked the assistant _____ the reservation.",
        choices: [
          "confirm",
          "to confirm",
          "confirming",
          "confirmed"
        ],
        answer: 1,
        structure:
          "S: Ms. Ito\n" +
          "V: asked\n" +
          "O: the assistant\n" +
          "C: to confirm the reservation",
        reason:
          "ask＋人＋to＋動詞の原形は「人に～するよう頼む」。" +
          "to confirm ... は the assistant が行う行為を示す" +
          "目的語の補語です。",
        options: [
          "A confirm：原形。ask＋人の直後には通常 to が必要。",
          "B to confirm：to不定詞。正解。",
          "C confirming：動名詞・現在分詞。この語法には合わない。",
          "D confirmed：過去形・過去分詞。この語法には合わない。"
        ],
        vocab: [
          "ask 人 to do：人に～するよう頼む",
          "confirm（他動詞）：～を確認する",
          "reservation（名詞）：予約"
        ],
        summary:
          "ask＋人＋to do＝人に～するよう頼む。" +
          "confirm the reservation＝予約を確認する。"
      },
      {
        id: "s01",
        level: "standard",
        topic: "接続詞と前置詞",
        question:
          "The proposal was approved _____ several concerns about its cost.",
        choices: [
          "although",
          "despite",
          "because",
          "whereas"
        ],
        answer: 1,
        structure:
          "S: The proposal\n" +
          "V: was approved\n" +
          "M: despite several concerns about its cost",
        reason:
          "空所の後は several concerns という名詞句です。" +
          "despite は前置詞で、despite＋名詞句" +
          "「～にもかかわらず」を作ります。" +
          "although / because / whereas は" +
          "後ろに原則として節（主語＋動詞）を取ります。",
        options: [
          "A although：接続詞「～だけれども」。後ろに節が必要。",
          "B despite：前置詞「～にもかかわらず」。正解。",
          "C because：接続詞「～なので」。後ろに節が必要。",
          "D whereas：接続詞「一方で」。後ろに節が必要。"
        ],
        vocab: [
          "proposal（名詞）：提案",
          "approve（他動詞）：～を承認する",
          "concern（名詞）：懸念",
          "despite＋名詞句：～にもかかわらず"
        ],
        summary:
          "despite＋名詞句／although＋節。" +
          "despite several concerns＝いくつかの懸念にもかかわらず。" +
          "proposal＝提案。"
      },
      {
        id: "s02",
        level: "standard",
        topic: "関係代名詞",
        question:
          "The supplier, _____ headquarters are in Osaka, " +
          "has opened a new warehouse.",
        choices: ["which", "whose", "where", "that"],
        answer: 1,
        structure:
          "主節 S: The supplier\n" +
          "主節 V: has opened\n" +
          "主節 O: a new warehouse\n" +
          "挿入節 S: whose headquarters\n" +
          "挿入節 V: are\n" +
          "挿入節 M: in Osaka",
        reason:
          "空所の直後の headquarters にかかる所有格が必要です。" +
          "whose headquarters で「その会社の本社」。" +
          "挿入された関係詞節は supplier を補足しています。",
        options: [
          "A which：関係代名詞「それは／それを」。名詞 headquarters を所有格として修飾できない。",
          "B whose：関係代名詞の所有格「その～の」。正解。",
          "C where：関係副詞「そこで」。名詞を直接修飾できない。",
          "D that：関係代名詞。所有格ではなく、通常このカンマ付きの関係詞節にも使わない。"
        ],
        vocab: [
          "supplier（名詞）：供給業者",
          "headquarters（名詞）：本社（形は複数形）",
          "warehouse（名詞）：倉庫",
          "open a warehouse：倉庫を開設する"
        ],
        summary:
          "whose＋名詞＝その～の。" +
          "whose headquarters are in Osaka＝本社が大阪にある。" +
          "warehouse＝倉庫。"
      },
      {
        id: "s03",
        level: "standard",
        topic: "前置詞の to",
        question:
          "We look forward to _____ with your team on the project.",
        choices: [
          "collaborate",
          "collaborating",
          "collaborated",
          "collaborative"
        ],
        answer: 1,
        structure:
          "S: We\n" +
          "V: look forward to\n" +
          "O: collaborating with your team on the project" +
          "（to の目的語となる動名詞句）",
        reason:
          "look forward to の to は不定詞の印ではなく前置詞です。" +
          "前置詞の後ろには名詞相当語が来るため、" +
          "動詞を置くなら collaborating という動名詞にします。",
        options: [
          "A collaborate：動詞の原形「協力する」。前置詞 to の直後には置けない。",
          "B collaborating：動名詞「協力すること」。正解。",
          "C collaborated：過去形・過去分詞。ここでは名詞相当語にならない。",
          "D collaborative：形容詞「協力的な」。単独でこの位置に置けない。"
        ],
        vocab: [
          "look forward to ～ing：～するのを楽しみにする",
          "collaborate with 人 on 事：人と事について協力する（自動詞）",
          "project（名詞）：企画、事業"
        ],
        summary:
          "look forward to の to は前置詞 → 動名詞 collaborating。" +
          "collaborate with 人 on 事＝人と事について協力する。"
      },
      {
        id: "s04",
        level: "standard",
        topic: "時を表す節",
        question:
          "The revised schedule will be sent to everyone " +
          "as soon as it _____ finalized.",
        choices: ["will be", "is", "has", "be"],
        answer: 1,
        structure:
          "主節 S: The revised schedule\n" +
          "主節 V: will be sent\n" +
          "主節 M: to everyone\n" +
          "時の節 S: it\n" +
          "時の節 V: is finalized",
        reason:
          "as soon as は「～するとすぐに」を表す接続詞です。" +
          "未来のことでも、時を表す従属節の中では" +
          "原則として現在形を使います。" +
          "schedule は「確定される」ので受動態 is finalized です。",
        options: [
          "A will be：未来の受動態。時を表す節内の未来表現としてはここでは使わない。",
          "B is：現在形の受動態 is finalized を作る。正解。",
          "C has：has finalized だと能動態になり、schedule が何かを確定する意味になる。",
          "D be：主語 it の後に単独では置けない。"
        ],
        vocab: [
          "revised（形容詞的な過去分詞）：改訂された",
          "schedule（名詞）：予定表",
          "finalize（他動詞）：～を確定する",
          "as soon as＋節：～するとすぐに"
        ],
        summary:
          "未来の話でも as soon as の節では現在形。" +
          "is finalized＝確定される。" +
          "revised schedule＝改訂された予定表。"
      },
      {
        id: "a01",
        level: "advanced",
        topic: "否定語の倒置",
        question:
          "Not until every attendee had signed in _____ the seminar begin.",
        choices: ["had", "did", "was", "does"],
        answer: 1,
        structure:
          "時の節 S: every attendee\n" +
          "時の節 V: had signed in\n" +
          "主節 S: the seminar\n" +
          "主節 V: did begin（通常語順では began）\n" +
          "M: Not until every attendee had signed in",
        reason:
          "Not until ... を文頭に出すと主節が倒置します。" +
          "通常の語順は The seminar did not begin until " +
          "every attendee had signed in. " +
          "ここでは過去の出来事なので " +
          "did＋主語＋動詞の原形 begin です。" +
          "had signed in はそれより前に完了した動作を示します。",
        options: [
          "A had：had the seminar begin とはできない。完了形なら begun が必要。",
          "B did：did the seminar begin という倒置を作る。正解。",
          "C was：was the seminar begin は動詞の形が合わない。",
          "D does：現在形。had signed in との時制が合わない。"
        ],
        vocab: [
          "Not until＋節＋did＋主語＋動詞の原形：～して初めて…した",
          "attendee（名詞）：参加者",
          "sign in（自動詞句）：受付を済ませる",
          "seminar（名詞）：セミナー"
        ],
        summary:
          "Not until を文頭に出すと主節が倒置。" +
          "過去なら did＋S＋動詞の原形。" +
          "sign in＝受付を済ませる。"
      },
      {
        id: "a02",
        level: "advanced",
        topic: "仮定法の倒置",
        question:
          "Had the vendor notified us earlier, " +
          "we _____ an alternative delivery date.",
        choices: [
          "can arrange",
          "could have arranged",
          "will arrange",
          "arrange"
        ],
        answer: 1,
        structure:
          "条件節 S: the vendor\n" +
          "条件節 V: had notified\n" +
          "条件節 O: us\n" +
          "条件節 M: earlier\n" +
          "主節 S: we\n" +
          "主節 V: could have arranged\n" +
          "主節 O: an alternative delivery date",
        reason:
          "Had the vendor notified ... は " +
          "If the vendor had notified ... の " +
          "if を省いて had を前に出した形です。" +
          "過去の事実と異なる仮定なので、主節は " +
          "could have＋過去分詞（～できただろうに）。" +
          "実際に通知があったかどうかは文法上の仮定として扱います。",
        options: [
          "A can arrange：現在の能力を表す形。過去の仮定と合わない。",
          "B could have arranged：過去の仮定の帰結を表す。正解。",
          "C will arrange：未来形。過去の仮定と合わない。",
          "D arrange：現在形。過去の仮定と合わない。"
        ],
        vocab: [
          "Had＋S＋過去分詞, S＋could have＋過去分詞：もし～していたら…できただろう",
          "notify 人（他動詞）：人に知らせる",
          "alternative（形容詞）：代わりの",
          "delivery date：納品日"
        ],
        summary:
          "Had＋S＋過去分詞＝If＋S＋had＋過去分詞。" +
          "過去の仮定 → could have arranged。" +
          "notify 人＝人に知らせる。"
      }
    ];
    const LABEL = {
      all: "全10問",
      basic: "基礎",
      standard: "標準",
      advanced: "800点以上",
      wrong: "間違い復習",
      saved: "保存した問題"
    };
    const LEVEL = {
      basic: "基礎",
      standard: "標準",
      advanced: "800点以上"
    };
    const KEY = "toeic-trainer-v1";
    let records = {};
    try {
      const stored = JSON.parse(localStorage.getItem(KEY) || "{}");
      if (stored && typeof stored === "object") {
        records = stored;
      }
    } catch (_error) {}
    let filter = "all";
    let session = null;
    const app = document.getElementById("app");
    const live = document.getElementById("live");
    const esc = value => String(value).replace(
      /[&<>"']/g,
      char => ({
        "&": "&amp;",
        "<": "&lt;",
        ">": "&gt;",
        "\"": "&quot;",
        "'": "&#39;"
      })[char]
    );
    const rec = id => records[id] || {
      attempts: 0,
      correct: 0,
      wrong: false,
      saved: false
    };
    function persist() {
      try {
        localStorage.setItem(KEY, JSON.stringify(records));
      } catch (_error) {
        live.textContent = "学習記録を保存できませんでした";
      }
    }
    function pool() {
      return QUESTIONS.filter(q =>
        filter === "all" ||
        q.level === filter ||
        (filter === "wrong" && rec(q.id).wrong) ||
        (filter === "saved" && rec(q.id).saved)
      );
    }
    function shuffle(items) {
      const result = [...items];
      for (let i = result.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [result[i], result[j]] = [result[j], result[i]];
      }
      return result;
    }
    function renderHome() {
      const all = Object.values(records);
      const attempts = all.reduce(
        (total, record) => total + (record.attempts || 0),
        0
      );
      const correct = all.reduce(
        (total, record) => total + (record.correct || 0),
        0
      );
      const count = pool().length;
      const wrongCount = QUESTIONS.filter(
        q => rec(q.id).wrong
      ).length;
      const filtersHTML = Object.keys(LABEL).map(key => {
        const number = QUESTIONS.filter(q =>
          key === q.level ||
          (key === "wrong" && rec(q.id).wrong) ||
          (key === "saved" && rec(q.id).saved)
        ).length;
        return `
          <button
            class="chip"
            data-action="filter"
            data-filter="${key}"
            aria-pressed="${filter === key}"
          >
            ${LABEL[key]}
            <span aria-hidden="true">
              ${key === "all" ? "" : `(${number})`}
            </span>
          </button>
        `;
      }).join("");
      app.innerHTML = `
        <section class="panel">
          <h2>今日の演習</h2>
          <p class="intro muted">
            難度または復習を選んで開始。
            出題順は毎回ランダムです。
            間違えた問題は正解するまで復習欄に残ります。
          </p>
          <div class="stats">
            <div class="stat">
              <strong>${attempts}</strong>
              <span>累計解答</span>
            </div>
            <div class="stat">
              <strong>
                ${attempts ? Math.round(correct / attempts * 100) : 0}%
              </strong>
              <span>累計正答率</span>
            </div>
            <div class="stat">
              <strong>${wrongCount}</strong>
              <span>要復習</span>
            </div>
          </div>
          <h2>出題範囲</h2>
          <div
            class="filters"
            role="group"
            aria-label="出題範囲"
          >
            ${filtersHTML}
          </div>
          <div class="row">
            <span class="muted small">${count}問を演習</span>
            <button
              class="primary"
              data-action="start"
              ${count ? "" : "disabled"}
            >
              演習を始める
            </button>
          </div>
        </section>
        <section class="panel small muted">
          収録数：基礎4問 · 標準4問 · 800点以上2問。
          Part 5形式のオリジナル問題です。
        </section>
      `;
    }
    function renderQuestion() {
      const q = session.items[session.index];
      const chosen = session.answers[q.id];
      const answered = chosen !== undefined;
      const saved = rec(q.id).saved;
      const choicesHTML = q.choices.map((choice, index) => {
        let stateClass = "";
        if (answered) {
          if (index === q.answer) {
            stateClass = "correct";
          } else if (index === chosen) {
            stateClass = "wrong";
          }
        }
        return `
          <button
            class="choice ${stateClass}"
            data-action="answer"
            data-choice="${index}"
            ${answered ? "disabled" : ""}
            aria-label="${"ABCD"[index]} ${esc(choice)}"
          >
            <b>${"ABCD"[index]}</b>
            <span>${esc(choice)}</span>
          </button>
        `;
      }).join("");
      app.innerHTML = `
        <section class="panel">
          <div class="row">
            <span class="badge ${q.level}">
              ${LEVEL[q.level]} · ${esc(q.topic)}
            </span>
            <span class="muted small">
              ${session.index + 1} / ${session.items.length}
            </span>
          </div>
          <div
            class="progress"
            role="progressbar"
            aria-label="進捗"
            aria-valuenow="${session.index + 1}"
            aria-valuemin="0"
            aria-valuemax="${session.items.length}"
          >
            <span
              style="width:${
                (session.index + 1) / session.items.length * 100
              }%"
            ></span>
          </div>
          <p class="question">${esc(q.question)}</p>
          <div
            class="choices"
            role="group"
            aria-label="選択肢"
          >
            ${choicesHTML}
          </div>
          ${
            answered
              ? renderFeedback(q, chosen, saved)
              : `
                <p class="muted small">
                  選択肢をタップすると採点します。
                  キーボードの A～D でも解答できます。
                </p>
              `
          }
        </section>
      `;
    }
    function renderFeedback(q, chosen, saved) {
      return `
        <div class="feedback">
          <div class="verdict ${chosen === q.answer ? "yes" : "no"}">
            ${chosen === q.answer ? "正解！" : "不正解"}
          </div>
          <p class="answer">
            正解：${"ABCD"[q.answer]} ${esc(q.choices[q.answer])}
          </p>
          <div class="block">
            <h3>文の構造（SVOC＋M）</h3>
            <p>${esc(q.structure)}</p>
          </div>
          <div class="block">
            <h3>なぜこの答え？</h3>
            <p>${esc(q.reason)}</p>
          </div>
          <h3>選択肢を確認</h3>
          <ul class="explain-list">
            ${q.options.map(
              option => `<li>${esc(option)}</li>`
            ).join("")}
          </ul>
          <h3>重要単語・語法・頻出表現</h3>
          <ul class="vocab">
            ${q.vocab.map(
              word => `<li>${esc(word)}</li>`
            ).join("")}
          </ul>
          <h3>コピー用まとめ</h3>
          <div class="copybox" id="summary">${esc(q.summary)}</div>
          <div class="actions">
            <button class="secondary" data-action="copy">
              まとめをコピー
            </button>
            <button class="secondary" data-action="save">
              ${saved ? "保存を解除" : "復習リストに保存"}
            </button>
            <button class="primary" data-action="next">
              ${
                session.index + 1 === session.items.length
                  ? "結果を見る"
                  : "次の問題へ"
              }
            </button>
          </div>
        </div>
      `;
    }
    function renderResult() {
      const done = session.items.map(q => ({
        q,
        answer: session.answers[q.id]
      }));
      const correct = done.filter(
        item => item.answer === item.q.answer
      ).length;
      const resultsHTML = [
        "basic",
        "standard",
        "advanced"
      ].map(level => {
        const sub = done.filter(
          item => item.q.level === level
        );
        const subCorrect = sub.filter(
          item => item.answer === item.q.answer
        ).length;
        return `
          <div>
            ${LEVEL[level]}
            <b>${subCorrect} / ${sub.length}</b>
          </div>
        `;
      }).join("");
      app.innerHTML = `
        <section class="panel">
          <span class="badge">演習完了</span>
          <h2 style="margin-top:16px">
            ${correct} / ${done.length} 問正解
          </h2>
          <p class="muted">
            今回の正答率：
            ${Math.round(correct / done.length * 100)}%
          </p>
          <div class="result-grid">
            ${resultsHTML}
          </div>
          <p class="small muted">
            間違えた問題は「間違い復習」から繰り返せます。
            復習で正解すると一覧から外れます。
          </p>
          <div class="actions">
            <button class="primary" data-action="home">
              範囲選択に戻る
            </button>
          </div>
        </section>
      `;
    }
    function render() {
      if (!session) {
        renderHome();
      } else if (session.index >= session.items.length) {
        renderResult();
      } else {
        renderQuestion();
      }
    }
    app.addEventListener("click", async event => {
      const button = event.target.closest("button[data-action]");
      if (!button) return;
      const action = button.dataset.action;
      if (action === "filter") {
        filter = button.dataset.filter;
        render();
        return;
      }
      if (action === "start") {
        const items = shuffle(pool());
        if (!items.length) return;
        session = {
          items,
          index: 0,
          answers: {}
        };
        render();
        return;
      }
      if (action === "home") {
        session = null;
        render();
        return;
      }
      if (!session || session.index >= session.items.length) {
        return;
      }
      const q = session.items[session.index];
      if (action === "answer") {
        if (session.answers[q.id] !== undefined) return;
        const selected = Number(button.dataset.choice);
        session.answers[q.id] = selected;
        const old = rec(q.id);
        records[q.id] = {
          ...old,
          attempts: (old.attempts || 0) + 1,
          correct:
            (old.correct || 0) + (selected === q.answer ? 1 : 0),
          wrong: selected !== q.answer
        };
        persist();
        render();
        live.textContent = selected === q.answer
          ? "正解です。解説を表示しました"
          : "不正解です。解説を表示しました";
        return;
      }
      if (action === "next") {
        session.index++;
        render();
        scrollTo({ top: 0, behavior: "smooth" });
        return;
      }
      if (action === "save") {
        records[q.id] = {
          ...rec(q.id),
          saved: !rec(q.id).saved
        };
        persist();
        render();
        live.textContent = records[q.id].saved
          ? "復習リストに保存しました"
          : "保存を解除しました";
        return;
      }
      if (action === "copy") {
        try {
          await navigator.clipboard.writeText(q.summary);
          live.textContent = "まとめをコピーしました";
          button.textContent = "コピーしました";
        } catch (_error) {
          const area = document.createElement("textarea");
          area.value = q.summary;
          document.body.append(area);
          area.select();
          const copied = document.execCommand("copy");
          area.remove();
          live.textContent = copied
            ? "まとめをコピーしました"
            : "コピーできませんでした。まとめを長押しして選択してください";
          if (copied) {
            button.textContent = "コピーしました";
          }
        }
      }
    });
    document.addEventListener("keydown", event => {
      if (
        !session ||
        session.index >= session.items.length ||
        event.altKey ||
        event.ctrlKey ||
        event.metaKey ||
        /INPUT|TEXTAREA/.test(document.activeElement.tagName)
      ) {
        return;
      }
      const index = "abcd".indexOf(event.key.toLowerCase());
      if (index < 0) return;
      const button = app.querySelector(
        `[data-action="answer"][data-choice="${index}"]`
      );
      if (button && !button.disabled) {
        button.click();
      }
    });
    render();
  </script>
</body>
</html>
