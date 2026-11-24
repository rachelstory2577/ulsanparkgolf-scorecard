
# ulsanparkgolf-scorecardnode_modules/
build/
dist/
coverage/
.DS_Store
*.log
.env*
!.env.example

<!doctype html>
<html lang="ko">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>즐거운 파크골프 스코어 카드</title>
    <meta
      name="description"
      content="울산 태화강·두동(둥동)·영천 웨스트우드 등 150km 파크골프장 선택, 귀엽고 선명한 선수 4칸 스코어카드, A·B·C·D 자동 합계 및 손가락 서명란"
    />
    <meta property="og:title" content="즐거운 파크골프 스코어 카드" />
    <meta
      property="og:description"
      content="울산 기준 150km 파크골프장 구장별 선택, 귀엽고 보기 쉬운 선수 4칸 스코어카드, A·B·C·D 자동 합계, 손가락 서명란"
    />
    <meta property="og:type" content="website" />
    <style>
      :root {
        --bg-canvas: #fbf8ee;
        --surface-card: #ffffff;
        --surface-mint: #ebf6ee;
        --surface-mint-deep: #d6eedc;
        --surface-butter: #fff7cc;
        --accent-sunny: #ffe24a;
        --accent-sunny-hover: #f5d328;
        --accent-green: #18623d;
        --accent-green-hover: #11492d;
        --border-soft: #cde0d1;
        --border-strong: #87b594;
        --ink-primary: #17271d;
        --ink-secondary: #344e3d;
        --ink-muted: #5b7463;
        --under-bg: #dff6e5;
        --under-ink: #12562d;
        --even-bg: #f1f5f2;
        --even-ink: #2c4334;
        --over-bg: #ffebe5;
        --over-ink: #a32f1b;
        --hio-bg: #ffe98a;
        --hio-ink: #6e3d00;
        --danger: #b42d18;
        --focus-ring: #0f5132;
        --course-a: #e04f4f;
        --course-b: #3478e5;
        --course-c: #d98a12;
        --course-d: #4b5d6b;
        --cap-0: #ff7b72;
        --cap-1: #4da3ff;
        --cap-2: #f5b700;
        --cap-3: #36b37e;
        --radius-xl: 26px;
        --radius-lg: 20px;
        --radius-md: 15px;
        --radius-sm: 11px;
      }

      * {
        box-sizing: border-box;
      }

      html {
        font-size: 18px;
        -webkit-text-size-adjust: 100%;
      }

      body {
        margin: 0;
        padding: 0;
        background-color: var(--bg-canvas);
        background-image: radial-gradient(
          circle at 12% 0%,
          #eef8f0 0%,
          transparent 42%
        );
        color: var(--ink-primary);
        font-family:
          "Pretendard",
          "Apple SD Gothic Neo",
          "Malgun Gothic",
          "Noto Sans KR",
          -apple-system,
          BlinkMacSystemFont,
          sans-serif;
        line-height: 1.5;
        min-height: 100vh;
      }

      button,
      input,
      select,
      textarea {
        font-family: inherit;
      }

      button {
        cursor: pointer;
        border: none;
        touch-action: manipulation;
        user-select: none;
        -webkit-tap-highlight-color: transparent;
        transition:
          transform 140ms cubic-bezier(0.16, 1, 0.3, 1),
          background-color 140ms ease,
          border-color 140ms ease,
          box-shadow 140ms ease;
      }

      button:active:not(:disabled) {
        transform: scale(0.96);
      }

      button:focus-visible,
      input:focus-visible,
      select:focus-visible,
      textarea:focus-visible {
        outline: 3px solid var(--focus-ring);
        outline-offset: 2px;
      }

      .app-container {
        max-width: 1260px;
        margin: 0 auto;
        padding: 18px 16px 38px;
        display: flex;
        flex-direction: column;
        gap: 20px;
      }

      /* 1. 상단 헤더 (귀여운 파크골프 캐릭터 + 햇살 옐로우 포인트) */
      #Header_Title {
        background-color: var(--surface-mint);
        border: 2px solid var(--border-soft);
        border-radius: var(--radius-xl);
        padding: 18px 22px;
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        justify-content: space-between;
        gap: 14px;
        box-shadow: 0 4px 0 #d5e8d9;
      }

      .header-brand-wrap {
        display: flex;
        align-items: center;
        gap: 14px;
      }

      .mascot-badge {
        width: 64px;
        height: 64px;
        border-radius: 20px;
        background-color: var(--accent-sunny);
        border: 2px solid #e6c62e;
        display: flex;
        align-items: center;
        justify-content: center;
        flex-shrink: 0;
        box-shadow: 0 3px 0 #d8b51d;
      }

      .header-brand {
        display: flex;
        flex-direction: column;
        gap: 4px;
      }

      .header-title {
        margin: 0;
        font-size: clamp(1.32rem, 2.8vw, 1.85rem);
        font-weight: 900;
        letter-spacing: -0.025em;
        color: var(--ink-primary);
        line-height: 1.25;
      }

      .header-meta {
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        gap: 8px;
        font-size: 0.94rem;
        font-weight: 700;
        color: var(--ink-secondary);
      }

      .sound-toggle-btn {
        min-height: 48px;
        padding: 10px 18px;
        border-radius: 999px;
        background-color: var(--surface-card);
        border: 2px solid var(--border-strong);
        color: var(--ink-primary);
        font-size: 0.95rem;
        font-weight: 800;
        display: inline-flex;
        align-items: center;
        gap: 8px;
        white-space: nowrap;
        box-shadow: 0 2px 0 var(--border-soft);
      }

      .sound-toggle-btn[aria-pressed="false"] {
        background-color: #efecdf;
        color: var(--ink-muted);
        border-color: var(--border-soft);
      }

      /* 공통 카드 스타일 (부드러운 둥근 모서리 + 몽글몽글한 입체 바닥선) */
      .section-card {
        background-color: var(--surface-card);
        border: 2px solid var(--border-soft);
        border-radius: var(--radius-xl);
        padding: 20px;
        box-shadow: 0 4px 0 #e5eade;
      }

      .section-header {
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        justify-content: space-between;
        gap: 12px;
        margin-bottom: 16px;
        padding-bottom: 12px;
        border-bottom: 2px dashed #e3ebd8;
      }

      .section-title-row {
        display: flex;
        align-items: center;
        gap: 10px;
      }

      .section-icon-dot {
        width: 34px;
        height: 34px;
        border-radius: 12px;
        background-color: var(--surface-butter);
        border: 1.5px solid #edd053;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        flex-shrink: 0;
      }

      .section-title {
        margin: 0;
        font-size: 1.2rem;
        font-weight: 900;
        color: var(--ink-primary);
        letter-spacing: -0.015em;
      }

      .section-subtitle {
        display: block;
        margin-top: 3px;
        font-size: 0.88rem;
        font-weight: 600;
        color: var(--ink-muted);
      }

      /* 2. 구장 선택 영역 (Course_Selector) */
      .region-filter-bar {
        display: flex;
        flex-wrap: wrap;
        gap: 8px;
        margin-bottom: 14px;
      }

      .region-btn {
        min-height: 44px;
        padding: 8px 16px;
        border-radius: 999px;
        background-color: #f7f4e8;
        border: 1.5px solid var(--border-soft);
        color: var(--ink-secondary);
        font-size: 0.9rem;
        font-weight: 800;
        white-space: nowrap;
      }

      .region-btn.active {
        background-color: var(--accent-sunny);
        border-color: #d9b516;
        color: var(--ink-primary);
        box-shadow: 0 2px 0 #d9b516;
      }

      .course-select-grid {
        display: grid;
        grid-template-columns: 1fr;
        gap: 14px;
        align-items: start;
      }

      @media (min-width: 900px) {
        .course-select-grid {
          grid-template-columns: 1.05fr 0.95fr;
        }
      }

      .course-select-wrap {
        display: flex;
        flex-direction: column;
        gap: 10px;
      }

      .field-label {
        font-size: 0.92rem;
        font-weight: 800;
        color: var(--ink-secondary);
      }

      .course-select {
        width: 100%;
        min-height: 56px;
        padding: 12px 16px;
        font-size: 1rem;
        font-weight: 800;
        color: var(--ink-primary);
        background-color: #fdfbf2;
        border: 2px solid var(--border-strong);
        border-radius: var(--radius-md);
        cursor: pointer;
      }

      .text-input-lg {
        width: 100%;
        min-height: 52px;
        padding: 10px 14px;
        font-size: 1rem;
        font-weight: 700;
        color: var(--ink-primary);
        background-color: #fdfbf2;
        border: 2px solid var(--border-soft);
        border-radius: var(--radius-md);
      }

      .course-info-panel {
        background-color: var(--surface-mint);
        border: 1.5px solid var(--border-soft);
        border-radius: var(--radius-lg);
        padding: 15px 18px;
        display: flex;
        flex-direction: column;
        gap: 6px;
      }

      .course-info-title-row {
        display: flex;
        flex-wrap: wrap;
        align-items: baseline;
        justify-content: space-between;
        gap: 8px;
      }

      .course-info-name {
        font-size: 1.12rem;
        font-weight: 900;
        color: var(--ink-primary);
      }

      .course-info-distance {
        font-size: 0.92rem;
        font-weight: 900;
        color: var(--accent-green);
      }

      .course-info-meta {
        font-size: 0.9rem;
        font-weight: 700;
        color: var(--ink-secondary);
      }

      .course-info-note {
        font-size: 0.85rem;
        font-weight: 600;
        color: var(--ink-muted);
      }

      .custom-course-input-row {
        display: none;
        flex-direction: column;
        gap: 6px;
      }

      .custom-course-input-row.visible {
        display: flex;
      }

      /* 3. 메인 스코어카드 표 (상단 4칸 선수 + 좌측 A 1번 파3 형식) */
      .scorecard-toolbar {
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        justify-content: space-between;
        gap: 12px;
        margin-bottom: 14px;
      }

      .course-tabs-bar {
        display: flex;
        flex-wrap: wrap;
        gap: 8px;
      }

      .course-tab-btn {
        min-height: 48px;
        padding: 8px 16px;
        border-radius: 999px;
        background-color: #f6f3e6;
        border: 1.5px solid var(--border-soft);
        color: var(--ink-primary);
        font-size: 0.95rem;
        font-weight: 800;
        white-space: nowrap;
        display: inline-flex;
        align-items: center;
        gap: 6px;
      }

      .course-tab-btn.active {
        background-color: var(--accent-green);
        border-color: var(--accent-green);
        color: #ffffff;
        box-shadow: 0 3px 0 #0e3e26;
      }

      .player-count-bar {
        display: flex;
        align-items: center;
        gap: 5px;
        background-color: var(--surface-mint);
        padding: 5px;
        border-radius: 999px;
        border: 1.5px solid var(--border-soft);
      }

      .count-btn {
        min-height: 44px;
        min-width: 52px;
        padding: 8px 12px;
        border-radius: 999px;
        background-color: transparent;
        color: var(--ink-secondary);
        font-size: 0.92rem;
        font-weight: 800;
        white-space: nowrap;
      }

      .count-btn.active {
        background-color: var(--accent-sunny);
        color: var(--ink-primary);
        box-shadow: 0 2px 0 #d9b516;
      }

      .matrix-scroll-wrap {
        border: 2px solid var(--border-strong);
        border-radius: var(--radius-lg);
        overflow-x: auto;
        background-color: var(--surface-card);
      }

      .matrix-table {
        width: 100%;
        border-collapse: collapse;
        table-layout: fixed;
        min-width: 340px;
        font-variant-numeric: tabular-nums;
      }

      .matrix-table th,
      .matrix-table td {
        border-bottom: 1.5px solid #e7ebdf;
        border-right: 1.5px solid #e7ebdf;
        padding: 8px 6px;
        vertical-align: middle;
      }

      .matrix-table tr:last-child td {
        border-bottom: none;
      }

      .matrix-table th:last-child,
      .matrix-table td:last-child {
        border-right: none;
      }

      .col-hole {
        width: 148px;
        background-color: #f8f6ea;
      }

      /* 상단 4칸 선수 헤더 */
      .matrix-thead th {
        background-color: var(--surface-mint);
        padding: 12px 6px;
        border-bottom: 2px solid var(--border-strong);
        text-align: center;
      }

      .matrix-thead th.col-hole {
        background-color: var(--surface-mint-deep);
        font-size: 0.95rem;
        font-weight: 900;
        color: var(--ink-primary);
      }

      .player-col-header {
        display: flex;
        flex-direction: column;
        gap: 5px;
        align-items: center;
      }

      .player-cap-badge {
        display: inline-flex;
        align-items: center;
        gap: 5px;
        font-size: 0.78rem;
        font-weight: 900;
        color: var(--ink-primary);
      }

      .cap-dot {
        width: 14px;
        height: 14px;
        border-radius: 50%;
        border: 1.5px solid rgba(0, 0, 0, 0.2);
        display: inline-block;
      }

      .cap-0 { background-color: var(--cap-0); }
      .cap-1 { background-color: var(--cap-1); }
      .cap-2 { background-color: var(--cap-2); }
      .cap-3 { background-color: var(--cap-3); }

      .player-header-input {
        width: 100%;
        min-height: 44px;
        padding: 6px 8px;
        text-align: center;
        font-size: 16px;
        font-weight: 800;
        color: var(--ink-primary);
        background-color: #ffffff;
        border: 2px solid var(--border-strong);
        border-radius: var(--radius-sm);
      }

      .player-header-input:focus {
        border-color: var(--accent-green);
      }

      /* 좌측 홀 + 파 셀 */
      .hole-cell {
        background-color: #faf7ea;
        padding: 8px 10px !important;
      }

      .hole-cell-inner {
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: 6px;
      }

      .hole-name-group {
        display: flex;
        align-items: center;
        gap: 6px;
        white-space: nowrap;
      }

      .course-letter-mark {
        display: inline-flex;
        align-items: center;
        justify-content: center;
        width: 28px;
        height: 28px;
        border-radius: 9px;
        font-size: 0.88rem;
        font-weight: 900;
        color: #ffffff;
        flex-shrink: 0;
      }

      .mark-A { background-color: var(--course-a); }
      .mark-B { background-color: var(--course-b); }
      .mark-C { background-color: var(--course-c); }
      .mark-D { background-color: var(--course-d); }

      .hole-num-label {
        font-size: 1rem;
        font-weight: 900;
        color: var(--ink-primary);
      }

      .par-cycle-btn {
        min-height: 40px;
        min-width: 52px;
        padding: 4px 8px;
        border-radius: 999px;
        background-color: #ffffff;
        border: 1.5px solid var(--border-strong);
        color: var(--ink-primary);
        font-size: 0.88rem;
        font-weight: 900;
        white-space: nowrap;
      }

      .par-cycle-btn.par-5 {
        background-color: var(--surface-butter);
        border-color: #d99b06;
        color: #704100;
      }

      .par-cycle-btn.par-3 {
        background-color: var(--surface-mint);
        border-color: #5a9c6d;
        color: #12562d;
      }

      /* 타수 입력 셀 */
      .score-cell {
        text-align: center;
        padding: 6px !important;
        background-color: var(--surface-card);
      }

      .score-cell.is-hio {
        background-color: var(--hio-bg);
      }

      .score-cell.is-under {
        background-color: var(--under-bg);
      }

      .score-cell.is-over {
        background-color: var(--over-bg);
      }

      .score-cell.is-active-target {
        box-shadow: inset 0 0 0 3px var(--accent-green);
      }

      .cell-stepper {
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 6px;
      }

      .cell-step-btn {
        width: 42px;
        height: 44px;
        border-radius: 12px;
        font-size: 1.35rem;
        font-weight: 900;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        line-height: 1;
        flex-shrink: 0;
      }

      .cell-step-minus {
        background-color: #f6f3e4;
        border: 1.5px solid var(--border-strong);
        color: var(--ink-primary);
      }

      .cell-step-minus:disabled {
        opacity: 0.35;
        cursor: not-allowed;
      }

      .cell-step-plus {
        background-color: var(--accent-green);
        color: #ffffff;
        box-shadow: 0 2px 0 #0e3d25;
      }

      .cell-score-trigger {
        min-width: 52px;
        min-height: 50px;
        padding: 4px 6px;
        border-radius: 12px;
        background-color: transparent;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        gap: 1px;
      }

      .cell-score-trigger:hover {
        background-color: rgba(24, 98, 61, 0.08);
      }

      .cell-score-num {
        font-size: 1.48rem;
        font-weight: 900;
        color: var(--ink-primary);
        line-height: 1.05;
      }

      .cell-score-num.is-empty {
        color: #93a396;
        font-size: 1.2rem;
      }

      .cell-score-tag {
        font-size: 0.72rem;
        font-weight: 900;
        white-space: nowrap;
      }

      .tag-hio { color: var(--hio-ink); }
      .tag-under { color: var(--under-ink); }
      .tag-even { color: var(--even-ink); }
      .tag-over { color: var(--over-ink); }

      /* 코스 소계 행 & 전체 총합계 행 */
      .subtotal-row td {
        background-color: var(--surface-mint);
        font-weight: 900;
        padding: 12px 6px !important;
        border-top: 2px solid var(--border-strong);
        border-bottom: 2px solid var(--border-strong);
        text-align: center;
      }

      .subtotal-row td.hole-cell {
        text-align: left;
        padding-left: 12px !important;
        font-size: 0.96rem;
        color: var(--ink-primary);
      }

      .grandtotal-row td {
        background-color: var(--accent-green);
        color: #ffffff;
        font-weight: 900;
        padding: 14px 6px !important;
        text-align: center;
        border-right-color: rgba(255, 255, 255, 0.22);
      }

      .grandtotal-row td.hole-cell {
        background-color: var(--accent-green-hover);
        color: #ffffff;
        text-align: left;
        padding-left: 12px !important;
      }

      .rank-summary-row td {
        background-color: var(--accent-sunny);
        color: var(--ink-primary);
        font-weight: 900;
        padding: 12px 6px !important;
        text-align: center;
        font-size: 1.02rem;
      }

      .rank-summary-row td.hole-cell {
        background-color: #f5d328;
        text-align: left;
        padding-left: 12px !important;
      }

      .sum-main-num {
        font-size: 1.25rem;
        font-weight: 900;
        line-height: 1.15;
      }

      .sum-sub-diff {
        font-size: 0.78rem;
        font-weight: 800;
        opacity: 0.92;
      }

      /* 하단 2열 영역 (실시간 순위 + 서명란) */
      .bottom-two-col {
        display: grid;
        grid-template-columns: 1fr;
        gap: 20px;
        align-items: start;
      }

      @media (min-width: 960px) {
        .bottom-two-col {
          grid-template-columns: 1fr 1fr;
        }
      }

      .leaderboard-list {
        display: flex;
        flex-direction: column;
        gap: 10px;
      }

      .rank-row {
        display: grid;
        grid-template-columns: 74px 1fr auto;
        align-items: center;
        gap: 12px;
        padding: 14px 16px;
        background-color: #fbf9f0;
        border: 1.5px solid var(--border-soft);
        border-radius: var(--radius-lg);
      }

      .rank-row.rank-first {
        background-color: var(--surface-butter);
        border-color: #e6c12e;
      }

      .rank-position {
        height: 48px;
        border-radius: 14px;
        background-color: var(--surface-card);
        border: 1.5px solid var(--border-soft);
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 4px;
        font-size: 1.02rem;
        font-weight: 900;
        color: var(--ink-primary);
        font-variant-numeric: tabular-nums;
      }

      .rank-first .rank-position {
        background-color: var(--accent-sunny);
        border-color: #d4ad12;
        color: var(--ink-primary);
      }

      .rank-player-meta {
        display: flex;
        flex-direction: column;
        gap: 2px;
        min-width: 0;
      }

      .rank-player-name {
        font-size: 1.12rem;
        font-weight: 900;
        color: var(--ink-primary);
        overflow: hidden;
        text-overflow: ellipsis;
        white-space: nowrap;
      }

      .rank-course-breakdown {
        font-size: 0.85rem;
        font-weight: 700;
        color: var(--ink-secondary);
        font-variant-numeric: tabular-nums;
      }

      .rank-holes-played {
        font-size: 0.82rem;
        font-weight: 600;
        color: var(--ink-muted);
      }

      .rank-score-summary {
        text-align: right;
        display: flex;
        flex-direction: column;
        align-items: flex-end;
        gap: 2px;
      }

      .rank-total-strokes {
        font-size: 1.45rem;
        font-weight: 900;
        color: var(--ink-primary);
        font-variant-numeric: tabular-nums;
        line-height: 1.1;
      }

      .rank-par-diff {
        font-size: 0.9rem;
        font-weight: 800;
        font-variant-numeric: tabular-nums;
      }

      .diff-under { color: var(--under-ink); }
      .diff-even { color: var(--ink-secondary); }
      .diff-over { color: var(--over-ink); }

      /* 서명란 */
      .signer-tabs {
        display: flex;
        flex-wrap: wrap;
        gap: 8px;
        margin-bottom: 14px;
      }

      .signer-tab-btn {
        min-height: 44px;
        padding: 8px 14px;
        border-radius: 999px;
        background-color: #f6f3e6;
        border: 1.5px solid var(--border-soft);
        color: var(--ink-secondary);
        font-size: 0.9rem;
        font-weight: 800;
        white-space: nowrap;
      }

      .signer-tab-btn.signed {
        border-color: var(--accent-green);
        background-color: var(--under-bg);
        color: var(--under-ink);
      }

      .signer-tab-btn.active {
        background-color: var(--accent-green);
        border-color: var(--accent-green);
        color: #ffffff;
      }

      .signature-pad-shell {
        position: relative;
        background-color: #fefdf8;
        border: 2.5px dashed var(--border-strong);
        border-radius: var(--radius-lg);
        overflow: hidden;
        height: 185px;
        touch-action: none;
      }

      .signature-canvas {
        display: block;
        width: 100%;
        height: 100%;
        cursor: crosshair;
        touch-action: none;
      }

      .signature-placeholder {
        position: absolute;
        inset: 0;
        display: flex;
        align-items: center;
        justify-content: center;
        pointer-events: none;
        font-size: 1rem;
        font-weight: 700;
        color: #7c9282;
        text-align: center;
        padding: 16px;
      }

      .signature-placeholder.hidden {
        display: none;
      }

      .signature-actions-row {
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        justify-content: space-between;
        gap: 10px;
        margin-top: 12px;
      }

      .sign-status-text {
        font-size: 0.9rem;
        font-weight: 700;
        color: var(--ink-secondary);
      }

      .sign-clear-btn {
        min-height: 46px;
        padding: 8px 18px;
        border-radius: 999px;
        background-color: #fff0ec;
        border: 1.5px solid #e6a89c;
        color: var(--danger);
        font-size: 0.95rem;
        font-weight: 800;
        white-space: nowrap;
      }

      .saved-signatures-gallery {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
        gap: 10px;
        margin-top: 14px;
      }

      .saved-sign-card {
        background-color: #fbf9f0;
        border: 1.5px solid var(--border-soft);
        border-radius: var(--radius-md);
        padding: 8px;
        display: flex;
        flex-direction: column;
        gap: 4px;
      }

      .saved-sign-label {
        font-size: 0.8rem;
        font-weight: 800;
        color: var(--ink-secondary);
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
      }

      .saved-sign-preview {
        height: 52px;
        background-color: #ffffff;
        border: 1px solid #e5e2d3;
        border-radius: 8px;
        display: flex;
        align-items: center;
        justify-content: center;
        overflow: hidden;
        font-size: 0.76rem;
        color: var(--ink-muted);
      }

      .saved-sign-preview img {
        max-width: 100%;
        max-height: 100%;
        object-fit: contain;
      }

      /* 하단 관리 버튼 (Action_Footer) */
      #Action_Footer {
        background-color: var(--surface-card);
        border: 2px solid var(--border-soft);
        border-radius: var(--radius-xl);
        padding: 20px;
        display: grid;
        grid-template-columns: repeat(3, minmax(0, 1fr));
        gap: 14px;
        box-shadow: 0 4px 0 #e5eade;
      }

      .footer-btn {
        min-height: 60px;
        padding: 14px 18px;
        border-radius: var(--radius-md);
        font-size: 1.05rem;
        font-weight: 900;
        display: inline-flex;
        align-items: center;
        justify-content: center;
        gap: 8px;
        white-space: nowrap;
      }

      .btn-save {
        background-color: var(--accent-green);
        color: #ffffff;
        box-shadow: 0 4px 0 #0e3d25;
      }

      .btn-save:hover {
        background-color: var(--accent-green-hover);
      }

      .btn-copy {
        background-color: var(--accent-sunny);
        border: 1.5px solid #d9b516;
        color: var(--ink-primary);
        box-shadow: 0 4px 0 #d9b516;
      }

      .btn-copy:hover {
        background-color: var(--accent-sunny-hover);
      }

      .btn-reset {
        background-color: #fff0ec;
        border: 1.5px solid #e6a89c;
        color: var(--danger);
        box-shadow: 0 4px 0 #e6b8ae;
      }

      .btn-reset:hover {
        background-color: #ffe2da;
      }

      /* 큰 손가락 타수 입력 시트 */
      .keypad-backdrop {
        position: fixed;
        inset: 0;
        background-color: rgba(19, 36, 25, 0.48);
        display: none;
        align-items: flex-end;
        justify-content: center;
        z-index: 75;
      }

      .keypad-backdrop.open {
        display: flex;
      }

      .keypad-sheet {
        background-color: var(--surface-card);
        border-top: 4px solid var(--accent-sunny);
        border-radius: 28px 28px 0 0;
        width: 100%;
        max-width: 560px;
        padding: 20px 18px 26px;
        display: flex;
        flex-direction: column;
        gap: 14px;
        box-shadow: 0 -10px 30px rgba(19, 36, 25, 0.22);
      }

      .keypad-header {
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: 10px;
      }

      .keypad-title {
        font-size: 1.18rem;
        font-weight: 900;
        color: var(--ink-primary);
      }

      .keypad-close-btn {
        min-height: 44px;
        padding: 8px 18px;
        border-radius: 999px;
        background-color: var(--accent-sunny);
        color: var(--ink-primary);
        font-size: 0.95rem;
        font-weight: 900;
      }

      .keypad-stepper-row {
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 18px;
        background-color: var(--surface-mint);
        padding: 12px;
        border-radius: var(--radius-lg);
      }

      .keypad-step-btn {
        width: 68px;
        height: 68px;
        border-radius: 18px;
        font-size: 2rem;
        font-weight: 900;
        display: inline-flex;
        align-items: center;
        justify-content: center;
      }

      .keypad-current-val {
        min-width: 90px;
        text-align: center;
        display: flex;
        flex-direction: column;
        align-items: center;
      }

      .keypad-big-num {
        font-size: 2.4rem;
        font-weight: 900;
        line-height: 1.05;
        font-variant-numeric: tabular-nums;
      }

      .keypad-eval-text {
        font-size: 0.9rem;
        font-weight: 900;
        color: var(--accent-green);
      }

      .keypad-quick-grid {
        display: grid;
        grid-template-columns: repeat(4, minmax(0, 1fr));
        gap: 10px;
      }

      .quick-num-btn {
        min-height: 58px;
        border-radius: 16px;
        background-color: #f8f5e8;
        border: 1.5px solid var(--border-strong);
        color: var(--ink-primary);
        font-size: 1.25rem;
        font-weight: 900;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        line-height: 1.1;
      }

      .quick-num-btn.active {
        background-color: var(--accent-green);
        border-color: var(--accent-green);
        color: #ffffff;
      }

      .quick-num-sub {
        font-size: 0.72rem;
        font-weight: 700;
        opacity: 0.88;
      }

      .keypad-nav-row {
        display: grid;
        grid-template-columns: 1fr 1fr;
        gap: 10px;
      }

      .keypad-nav-btn {
        min-height: 52px;
        border-radius: 16px;
        background-color: var(--surface-mint);
        border: 1.5px solid var(--border-strong);
        color: var(--ink-primary);
        font-size: 1rem;
        font-weight: 800;
      }

      /* 토스트 및 모달 */
      .toast-banner {
        position: fixed;
        left: 50%;
        bottom: 24px;
        transform: translateX(-50%) translateY(16px);
        background-color: var(--ink-primary);
        color: #ffffff;
        padding: 16px 24px;
        border-radius: 999px;
        font-size: 1.02rem;
        font-weight: 700;
        box-shadow: 0 10px 28px rgba(19, 36, 25, 0.25);
        z-index: 90;
        opacity: 0;
        pointer-events: none;
        max-width: calc(100vw - 32px);
        text-align: center;
        transition:
          opacity 180ms ease,
          transform 180ms cubic-bezier(0.16, 1, 0.3, 1);
      }

      .toast-banner.visible {
        opacity: 1;
        transform: translateX(-50%) translateY(0);
      }

      .modal-backdrop {
        position: fixed;
        inset: 0;
        background-color: rgba(19, 36, 25, 0.55);
        display: none;
        align-items: center;
        justify-content: center;
        padding: 20px;
        z-index: 85;
      }

      .modal-backdrop.open {
        display: flex;
      }

      .modal-box {
        background-color: var(--surface-card);
        border: 2.5px solid var(--border-strong);
        border-radius: var(--radius-xl);
        padding: 28px 24px;
        max-width: 480px;
        width: 100%;
        text-align: center;
        display: flex;
        flex-direction: column;
        gap: 16px;
      }

      .modal-box.hio-box {
        background-color: #fffbeb;
        border-color: #eab308;
      }

      .modal-title {
        margin: 0;
        font-size: 1.5rem;
        font-weight: 900;
        color: var(--ink-primary);
        line-height: 1.3;
      }

      .modal-desc {
        margin: 0;
        font-size: 1.02rem;
        font-weight: 600;
        color: var(--ink-secondary);
        line-height: 1.5;
      }

      .modal-actions {
        display: flex;
        flex-direction: column;
        gap: 10px;
        margin-top: 6px;
      }

      .modal-btn-primary {
        min-height: 56px;
        padding: 14px 20px;
        border-radius: var(--radius-md);
        background-color: var(--accent-green);
        color: #ffffff;
        font-size: 1.08rem;
        font-weight: 800;
      }

      .modal-btn-danger {
        min-height: 56px;
        padding: 14px 20px;
        border-radius: var(--radius-md);
        background-color: var(--danger);
        color: #ffffff;
        font-size: 1.08rem;
        font-weight: 800;
      }

      .modal-btn-secondary {
        min-height: 54px;
        padding: 12px 20px;
        border-radius: var(--radius-md);
        background-color: #efece0;
        color: var(--ink-primary);
        font-size: 1.02rem;
        font-weight: 700;
      }

      .share-fallback-area {
        width: 100%;
        min-height: 160px;
        padding: 12px;
        font-size: 0.95rem;
        line-height: 1.5;
        border-radius: var(--radius-sm);
        border: 1.5px solid var(--border-strong);
        background-color: #faf8f0;
        color: var(--ink-primary);
        resize: vertical;
      }

      @media (max-width: 900px) {
        .cell-step-btn {
          display: none;
        }
        .cell-score-trigger {
          width: 100%;
          min-height: 54px;
        }
        .col-hole {
          width: 94px;
        }
        .hole-cell {
          padding: 6px !important;
        }
        .hole-cell-inner {
          flex-direction: column;
          align-items: flex-start;
          gap: 4px;
        }
        .par-cycle-btn {
          width: 100%;
          min-height: 34px;
          font-size: 0.85rem;
        }
      }

      @media (max-width: 640px) {
        html {
          font-size: 16px;
        }
        .app-container {
          padding: 12px 10px 28px;
          gap: 14px;
        }
        .section-card {
          padding: 14px 12px;
          border-radius: 22px;
        }
        #Header_Title {
          padding: 16px 14px;
          border-radius: 22px;
        }
        .mascot-badge {
          width: 52px;
          height: 52px;
          border-radius: 16px;
        }
        .col-hole {
          width: 84px;
        }
        .player-header-input {
          padding: 6px 4px;
          font-size: 16px;
        }
        #Action_Footer {
          grid-template-columns: 1fr;
          padding: 16px 14px;
        }
      }

      @media (prefers-reduced-motion: reduce) {
        * {
          transition: none !important;
        }
      }
    </style>
  </head>
  <body>
    <div class="app-container">
      <!-- 1. 상단 헤더 영역 (Header_Title) -->
      <header id="Header_Title">
        <div class="header-brand-wrap">
          <!-- 오리지널 귀여운 파크골프 공 & 깃발 SVG 마스코트 -->
          <div class="mascot-badge" aria-hidden="true">
            <svg width="42" height="42" viewBox="0 0 48 48" fill="none">
              <path d="M13 40C18 37 30 37 36 40" stroke="#18623D" stroke-width="3" stroke-linecap="round" />
              <line x1="34" y1="8" x2="34" y2="38" stroke="#17271D" stroke-width="2.5" stroke-linecap="round" />
              <path d="M34 9L44 13.5L34 18V9Z" fill="#E04F4F" stroke="#17271D" stroke-width="1.8" stroke-linejoin="round" />
              <circle cx="20" cy="27" r="11" fill="#FFFFFF" stroke="#17271D" stroke-width="2.3" />
              <path d="M12 21C14 15.5 25 15.5 28 21" fill="#18623D" stroke="#17271D" stroke-width="2" />
              <path d="M27 21H32" stroke="#17271D" stroke-width="2.2" stroke-linecap="round" />
              <circle cx="16.5" cy="26.5" r="1.4" fill="#17271D" />
              <circle cx="23.5" cy="26.5" r="1.4" fill="#17271D" />
              <path d="M17.5 30C18.8 31.4 21.2 31.4 22.5 30" stroke="#17271D" stroke-width="1.8" stroke-linecap="round" />
              <circle cx="14" cy="28.5" r="1.5" fill="#FF9AA2" />
              <circle cx="26" cy="28.5" r="1.5" fill="#FF9AA2" />
            </svg>
          </div>
          <div class="header-brand">
            <h1 class="header-title">즐거운 파크골프 스코어 카드</h1>
            <div class="header-meta">
              <span id="todayDateText"></span>
              <span aria-hidden="true">·</span>
              <span id="headerCourseText">태화강 파크골프장</span>
              <span aria-hidden="true">·</span>
              <span id="courseSummaryText">A·B·C·D코스 (36홀)</span>
            </div>
          </div>
        </div>
        <button
          type="button"
          id="soundToggleBtn"
          class="sound-toggle-btn"
          aria-pressed="true"
        >
          <span id="soundIcon" aria-hidden="true">🔊</span>
          <span id="soundLabel">효과음 켜짐</span>
        </button>
      </header>

      <!-- 2. 울산 기준 150km 파크골프장 선택 영역 (Course_Selector) -->
      <section id="Course_Selector" class="section-card" aria-labelledby="courseSelectorHeading">
        <div class="section-header">
          <div class="section-title-row">
            <span class="section-icon-dot" aria-hidden="true">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                <path d="M12 21C12 21 18 14.8 18 10C18 6.686 15.314 4 12 4C8.686 4 6 6.686 6 10C6 14.8 12 21 12 21Z" fill="#18623D" stroke="#17271D" stroke-width="1.8" />
                <circle cx="12" cy="10" r="2.4" fill="#FFE24A" />
              </svg>
            </span>
            <div>
              <h2 id="courseSelectorHeading" class="section-title">
                울산 인근 파크골프장 고르기 (150km)
              </h2>
              <span class="section-subtitle">
                구장을 선택하면 코스(A·B·C·D)와 홀별 기준타수가 자동으로 맞춰집니다
              </span>
            </div>
          </div>
        </div>

        <div class="region-filter-bar" role="group" aria-label="지역별 구장 보기">
          <button type="button" class="region-btn active" data-region="all">전체 보기</button>
          <button type="button" class="region-btn" data-region="ulsan">울산</button>
          <button type="button" class="region-btn" data-region="gyeongbuk">
            경주·영천·포항·구미
          </button>
          <button type="button" class="region-btn" data-region="gyeongnam">
            양산·부산·밀양·창원·대구
          </button>
        </div>

        <div class="course-select-grid">
          <div class="course-select-wrap">
            <label class="field-label" for="courseSelect">구장 이름 선택</label>
            <select id="courseSelect" class="course-select"></select>

            <div id="customCourseRow" class="custom-course-input-row">
              <label class="field-label" for="customCourseInput">직접 구장 이름 입력</label>
              <input
                id="customCourseInput"
                class="text-input-lg"
                type="text"
                maxlength="24"
                placeholder="예: 우리동네 파크골프장"
              />
            </div>
          </div>

          <div class="course-info-panel">
            <div class="course-info-title-row">
              <span id="selectedCourseName" class="course-info-name"></span>
              <span id="selectedCourseDistance" class="course-info-distance"></span>
            </div>
            <div id="selectedCourseMeta" class="course-info-meta"></div>
            <div id="selectedCourseNote" class="course-info-note"></div>
          </div>
        </div>
      </section>

      <!-- 3. 스코어카드 기록표 (상단 4칸 선수 + 좌측 A 1번 파3 형식 + A·B·C·D 자동 합계) -->
      <section id="Score_Card" class="section-card" aria-labelledby="scoreCardHeading">
        <div class="section-header">
          <div class="section-title-row">
            <span class="section-icon-dot" aria-hidden="true">
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                <rect x="4" y="4" width="16" height="16" rx="4" fill="#FFFFFF" stroke="#17271D" stroke-width="1.8" />
                <path d="M8 10H16M8 14H13" stroke="#18623D" stroke-width="2" stroke-linecap="round" />
              </svg>
            </span>
            <div>
              <h2 id="scoreCardHeading" class="section-title">
                스코어카드 기록표 (상단 4명 · 좌측 홀)
              </h2>
              <span class="section-subtitle">
                위 4칸에서 이름을 고치고, 좌측 파(Par) 버튼을 눌러 파3·파4·파5를 맞출 수 있습니다
              </span>
            </div>
          </div>

          <div class="player-count-bar" role="group" aria-label="참여 인원 선택">
            <button type="button" class="count-btn" data-count="1">1명</button>
            <button type="button" class="count-btn" data-count="2">2명</button>
            <button type="button" class="count-btn" data-count="3">3명</button>
            <button type="button" class="count-btn active" data-count="4">4명</button>
          </div>
        </div>

        <div class="scorecard-toolbar">
          <div id="courseTabsBar" class="course-tabs-bar" role="group" aria-label="코스 보기 선택"></div>
        </div>

        <div class="matrix-scroll-wrap">
          <table class="matrix-table" id="scorecardMatrixTable"></table>
        </div>
      </section>

      <!-- 4. 실시간 순위 요약 & 경기 종료 서명란 -->
      <div class="bottom-two-col">
        <section id="Live_Leaderboard" class="section-card" aria-labelledby="leaderboardHeading">
          <div class="section-header">
            <div class="section-title-row">
              <span class="section-icon-dot" aria-hidden="true">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                  <path d="M7 5H17V10C17 12.761 14.761 15 12 15C9.239 15 7 12.761 7 10V5Z" fill="#FFE24A" stroke="#17271D" stroke-width="1.8" />
                  <path d="M12 15V19M8.5 19H15.5" stroke="#17271D" stroke-width="1.8" stroke-linecap="round" />
                </svg>
              </span>
              <div>
                <h2 id="leaderboardHeading" class="section-title">
                  실시간 순위 및 A·B·C·D 합계
                </h2>
                <span class="section-subtitle">타수가 적은 순서대로 자동 정렬됩니다</span>
              </div>
            </div>
          </div>
          <div id="leaderboardList" class="leaderboard-list"></div>
        </section>

        <section id="Sign_Area" class="section-card" aria-labelledby="signHeading">
          <div class="section-header">
            <div class="section-title-row">
              <span class="section-icon-dot" aria-hidden="true">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none">
                  <path d="M4 19H20M6 15L15.5 5.5C16.3 4.7 17.7 4.7 18.5 5.5C19.3 6.3 19.3 7.7 18.5 8.5L9 18H6V15Z" stroke="#17271D" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" fill="#D6EEDC" />
                </svg>
              </span>
              <div>
                <h2 id="signHeading" class="section-title">경기 종료 확인 서명란</h2>
                <span class="section-subtitle">
                  점수 확인 후 손가락으로 사인해 주세요 (자동 저장)
                </span>
              </div>
            </div>
          </div>

          <div id="signerTabs" class="signer-tabs" role="group" aria-label="서명할 사람 선택"></div>

          <div class="signature-pad-shell">
            <canvas id="signatureCanvas" class="signature-canvas"></canvas>
            <div id="signaturePlaceholder" class="signature-placeholder">
              이곳에 손가락으로 편하게 서명해 주세요
            </div>
          </div>

          <div class="signature-actions-row">
            <span id="signStatusText" class="sign-status-text"></span>
            <button type="button" id="clearSignatureBtn" class="sign-clear-btn">
              서명 지우기
            </button>
          </div>

          <div id="savedSignaturesGallery" class="saved-signatures-gallery"></div>
        </section>
      </div>

      <!-- 5. 하단 관리 버튼 영역 (Action_Footer) -->
      <footer id="Action_Footer" aria-label="기록 관리 및 공유">
        <button type="button" id="saveBtn" class="footer-btn btn-save">
          기록 저장하기
        </button>
        <button type="button" id="copyShareBtn" class="footer-btn btn-copy">
          카톡 공유용 복사하기
        </button>
        <button type="button" id="resetBtn" class="footer-btn btn-reset">
          새 게임 시작하기
        </button>
      </footer>
    </div>

    <!-- 큰 손가락 타수 입력 시트 -->
    <div
      id="scoreEntrySheet"
      class="keypad-backdrop"
      role="dialog"
      aria-modal="true"
      aria-labelledby="keypadTitle"
    >
      <div class="keypad-sheet">
        <div class="keypad-header">
          <div id="keypadTitle" class="keypad-title">A코스 1번 홀 · 1번 선수</div>
          <button type="button" id="keypadCloseBtn" class="keypad-close-btn">완료</button>
        </div>

        <div class="keypad-stepper-row">
          <button type="button" id="keypadMinusBtn" class="keypad-step-btn cell-step-minus">
            −
          </button>
          <div class="keypad-current-val">
            <span id="keypadBigNum" class="keypad-big-num">0</span>
            <span id="keypadEvalText" class="keypad-eval-text">입력 전</span>
          </div>
          <button type="button" id="keypadPlusBtn" class="keypad-step-btn cell-step-plus">
            +
          </button>
        </div>

        <div id="keypadQuickGrid" class="keypad-quick-grid"></div>

        <div class="keypad-nav-row">
          <button type="button" id="keypadNextPlayerBtn" class="keypad-nav-btn">
            다음 선수 ▷
          </button>
          <button type="button" id="keypadNextHoleBtn" class="keypad-nav-btn">
            다음 홀 ▼
          </button>
        </div>
      </div>
    </div>

    <!-- 알림 토스트 -->
    <div id="toastBanner" class="toast-banner" role="status" aria-live="polite"></div>

    <!-- 홀인원 축하 모달 -->
    <div
      id="holeInOneModal"
      class="modal-backdrop"
      role="dialog"
      aria-modal="true"
      aria-labelledby="hioModalTitle"
    >
      <div class="modal-box hio-box">
        <h3 id="hioModalTitle" class="modal-title">🎉 홀인원 축하합니다! 🎉</h3>
        <p id="hioModalDesc" class="modal-desc"></p>
        <div class="modal-actions">
          <button type="button" id="hioCloseBtn" class="modal-btn-primary">
            멋져요! 계속하기
          </button>
          <button type="button" id="hioReplayBtn" class="modal-btn-secondary">
            축하 소리 다시 듣기
          </button>
        </div>
      </div>
    </div>

    <!-- 새 게임 확인 모달 -->
    <div
      id="resetModal"
      class="modal-backdrop"
      role="dialog"
      aria-modal="true"
      aria-labelledby="resetModalTitle"
    >
      <div class="modal-box">
        <h3 id="resetModalTitle" class="modal-title">새 게임을 시작할까요?</h3>
        <p class="modal-desc">
          현재 입력된 A·B·C·D 코스의 모든 타수와 서명이 초기화됩니다.<br />
          구장과 선수 이름은 그대로 남길 수 있습니다.
        </p>
        <div class="modal-actions">
          <button type="button" id="confirmResetScoresBtn" class="modal-btn-danger">
            네, 점수·서명만 초기화하기
          </button>
          <button type="button" id="confirmResetAllBtn" class="modal-btn-secondary">
            선수 이름까지 모두 처음부터 시작
          </button>
          <button type="button" id="cancelResetBtn" class="modal-btn-primary">
            아니요, 돌아가기
          </button>
        </div>
      </div>
    </div>

    <!-- 클립보드 복사 폴백 모달 -->
    <div
      id="shareFallbackModal"
      class="modal-backdrop"
      role="dialog"
      aria-modal="true"
      aria-labelledby="shareFallbackTitle"
    >
      <div class="modal-box">
        <h3 id="shareFallbackTitle" class="modal-title">결과 공유 텍스트</h3>
        <p class="modal-desc">
          아래 글자를 길게 눌러 전체 복사한 뒤 카카오톡에 붙여넣어 주세요.
        </p>
        <textarea id="shareFallbackText" class="share-fallback-area" readonly></textarea>
        <div class="modal-actions">
          <button type="button" id="shareFallbackCopyBtn" class="modal-btn-primary">
            한 번 더 복사 시도하기
          </button>
          <button type="button" id="shareFallbackCloseBtn" class="modal-btn-secondary">
            닫기
          </button>
        </div>
      </div>
    </div>

    <script>
      (function () {
        "use strict";

        const STORAGE_KEY = "parkgolf_scorecard_ulsan_v3";
        const COURSE_KEYS = ["A", "B", "C", "D"];
        const DEFAULT_NAMES = ["1번 선수", "2번 선수", "3번 선수", "4번 선수"];

        const TAEHWAGANG_PAR = [4, 3, 4, 5, 3, 4, 3, 3, 4];
        const STD_PAR_A = [3, 4, 3, 4, 4, 5, 4, 3, 3];
        const STD_PAR_B = [4, 3, 4, 3, 5, 4, 3, 4, 3];
        const STD_PAR_C = [3, 4, 4, 3, 3, 5, 4, 3, 4];
        const STD_PAR_D = [4, 3, 3, 4, 5, 3, 4, 4, 3];

        const GOLF_COURSES = [
          {
            id: "taehwagang",
            region: "ulsan",
            name: "태화강 파크골프장",
            location: "울산 남구 신정동 391 (태화강 둔치)",
            distanceKm: 3,
            operator: "울산남구도시관리공단",
            courses: ["A", "B", "C", "D"],
            defaultPars: {
              A: [...TAEHWAGANG_PAR],
              B: [...TAEHWAGANG_PAR],
              C: [...TAEHWAGANG_PAR],
              D: [...TAEHWAGANG_PAR],
            },
            note: "36홀 (A·적색, B·청색, C·황색, D·백색, 각 코스 파33). 좌측 파 버튼을 눌러 현장 표지판에 맞게 바로 수정 가능합니다.",
          },
          {
            id: "dudong",
            region: "ulsan",
            name: "두동 파크골프장 (둥동)",
            location: "울산 울주군 두동면 두동로 1355-50 (구미리)",
            distanceKm: 18,
            operator: "두동일신랜드 파크골프장",
            courses: ["A", "B", "C", "D"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "울산 울주군 두동면 대규모 코스 (A·B·C·D 36홀 단위 기록, 총 38홀 규모). 좌측 파3·파4·파5 버튼으로 수정 시 자동 저장됩니다.",
          },
          {
            id: "dongcheon",
            region: "ulsan",
            name: "동천 파크골프장",
            location: "울산 중구 남외동 508-1 (동천강 수변)",
            distanceKm: 5,
            operator: "울산 중구청",
            courses: ["A", "B", "C"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "27홀 (A·B·C 각 9홀, 코스별 파33 기준). 동천강변 대표 구장.",
          },
          {
            id: "jinjang",
            region: "ulsan",
            name: "진장 파크골프장",
            location: "울산 북구 진장동 400",
            distanceKm: 7,
            operator: "울산 북구청",
            courses: ["A", "B", "C"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "27홀 (A·B·C 각 9홀, 코스별 파33 기준). 북구 진장동 구장.",
          },
          {
            id: "ulsangrand",
            region: "ulsan",
            name: "울산대공원 파크골프장",
            location: "울산 남구 대공원로 94",
            distanceKm: 4,
            operator: "울산광역시시설공단",
            courses: ["A", "B"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "18홀 (A·B 각 9홀, 총 파66 기준). 도심 공원형 구장.",
          },
          {
            id: "donggu",
            region: "ulsan",
            name: "동구(동부동) 파크골프장",
            location: "울산 동구 동부동 99-15 일원",
            distanceKm: 14,
            operator: "울산 동구청",
            courses: ["A", "B"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "18홀 (A·B 각 9홀, 총 파66 기준). 울산 동구 신설 구장.",
          },
          {
            id: "seonbawi",
            region: "ulsan",
            name: "선바위(범서) 파크골프장",
            location: "울산 울주군 범서읍 천상리 1041-77",
            distanceKm: 11,
            operator: "울주군시설관리공단",
            courses: ["A", "B"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "18홀 (A·B 각 9홀, 총 파66 기준). 태화강 상류 선바위 인근.",
          },
          {
            id: "cheongnyang",
            region: "ulsan",
            name: "청량 파크골프장",
            location: "울산 울주군 청량읍 덕하리 979-63",
            distanceKm: 12,
            operator: "울주군시설관리공단",
            courses: ["A", "B"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "18홀 (A·B 각 9홀, 총 파66 기준).",
          },
          {
            id: "ulju",
            region: "ulsan",
            name: "울주 파크골프장 (온양)",
            location: "울산 울주군 온양읍 고산리 511",
            distanceKm: 22,
            operator: "울주군시설관리공단",
            courses: ["A", "B", "C", "D"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "36홀 (A·B·C·D 각 9홀, 총 파132 기준).",
          },
          {
            id: "alcheon",
            region: "gyeongbuk",
            name: "경주 알천 파크골프장",
            location: "경북 경주시 구황동 7-1 (황성공원 인근)",
            distanceKm: 35,
            operator: "경주시시설관리공단",
            courses: ["A", "B"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "울산에서 약 35km · 18홀 (A·B 각 9홀, 총 파66 기준).",
          },
          {
            id: "westwood",
            region: "gyeongbuk",
            name: "영천 웨스트우드 파크골프장",
            location: "경북 영천시 (피닉스 웨스트우드 파크골프장)",
            distanceKm: 60,
            operator: "웨스트우드 파크골프장",
            courses: ["A", "B", "C"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "울산에서 약 60km · A·B·C 총 27홀 천연잔디 산지형 구장 (기존 파3 골프장 리모델링, 오르막·도그레그 코스).",
          },
          {
            id: "jokyo",
            region: "gyeongbuk",
            name: "영천 조교 파크골프장",
            location: "경북 영천시 조교동 (금호강 둔치)",
            distanceKm: 65,
            operator: "영천시",
            courses: ["A", "B", "C", "D"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "울산에서 약 65km · 공인 36홀 (A·B·C·D 각 9홀).",
          },
          {
            id: "gokgang",
            region: "gyeongbuk",
            name: "포항 곡강 파크골프장",
            location: "경북 포항시 북구 흥해읍 용전리 965",
            distanceKm: 65,
            operator: "포항시시설관리공단",
            courses: ["A", "B", "C", "D"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "울산에서 약 65km · 곡강천 둔치 36홀 (A·B·C·D 각 9홀).",
          },
          {
            id: "dongrak",
            region: "gyeongbuk",
            name: "구미 동락 파크골프장",
            location: "경북 구미시 진평동 (낙동강 동락공원)",
            distanceKm: 130,
            operator: "구미시시설공단 (대한파크골프협회 공인 1호)",
            courses: ["A", "B", "C", "D"],
            defaultPars: {
              A: [4, 3, 4, 3, 4, 4, 3, 3, 5],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "울산에서 약 130km · 36홀 (A코스 실측 파 4·3·4·3·4·4·3·3·5 반영).",
          },
          {
            id: "gumimega",
            region: "gyeongbuk",
            name: "구미 파크골프장 (선산 괴평)",
            location: "경북 구미시 선산읍 괴평리",
            distanceKm: 140,
            operator: "구미시",
            courses: ["A", "B", "C", "D"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "울산에서 약 140km · 경북 최대 규모 다코스 구장 (A·B·C·D 단위 기록).",
          },
          {
            id: "hwangsan",
            region: "gyeongnam",
            name: "양산 황산 파크골프장",
            location: "경남 양산시 물금읍 증산리 999 (황산공원)",
            distanceKm: 45,
            operator: "양산시시설관리공단",
            courses: ["A", "B", "C", "D"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "울산에서 약 45km · 낙동강 수변 공인 36홀 (A·B·C·D 각 9홀).",
          },
          {
            id: "hwamyeong",
            region: "gyeongnam",
            name: "부산 화명생태공원 파크골프장",
            location: "부산 북구 화명동 (낙동강 화명생태공원)",
            distanceKm: 50,
            operator: "부산광역시 낙동강관리본부",
            courses: ["A", "B", "C", "D"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "울산에서 약 50km · A·B·C·D 각 9홀 (파33 표준).",
          },
          {
            id: "daejeo",
            region: "gyeongnam",
            name: "부산 대저생태공원 파크골프장",
            location: "부산 강서구 대저동 (대저생태공원)",
            distanceKm: 55,
            operator: "부산광역시 낙동강관리본부",
            courses: ["A", "B", "C", "D"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "울산에서 약 55km · 대규모 90홀 구장 (A·B·C·D 36홀 단위 기록).",
          },
          {
            id: "samnak",
            region: "gyeongnam",
            name: "부산 삼락생태공원 파크골프장",
            location: "부산 사상구 삼락동 (삼락생태공원)",
            distanceKm: 60,
            operator: "부산광역시 낙동강관리본부",
            courses: ["A", "B", "C", "D"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "울산에서 약 60km · 공인 P3 다이나믹 구장 기준 A·B·C·D 36홀.",
          },
          {
            id: "miryang",
            region: "gyeongnam",
            name: "밀양 삼문 파크골프장",
            location: "경남 밀양시 삼문동 631 (밀양강 수변)",
            distanceKm: 60,
            operator: "밀양시시설관리공단",
            courses: ["A", "B", "C", "D"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "울산에서 약 60km · 밀양강변 공인 A·B·C·D 36홀.",
          },
          {
            id: "sulmoe",
            region: "gyeongnam",
            name: "김해 한림 술뫼 파크골프장",
            location: "경남 김해시 한림면 시산리 일원",
            distanceKm: 70,
            operator: "김해시",
            courses: ["A", "B", "C", "D"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "울산에서 약 70km · 전국 최대급 90홀 구장 (A·B·C·D 36홀 단위 기록).",
          },
          {
            id: "daesan",
            region: "gyeongnam",
            name: "창원 대산 파크골프장",
            location: "경남 창원시 의창구 대산면 북부리 195-3",
            distanceKm: 80,
            operator: "창원시설공단",
            courses: ["A", "B", "C", "D"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "울산에서 약 80km · 1·2구장 A·B·C·D 각 9홀 (파33 표준).",
          },
          {
            id: "daegugangbyeon",
            region: "gyeongnam",
            name: "대구 강변(금호강) 파크골프장",
            location: "대구 북구 서변동 (금호강 둔치)",
            distanceKm: 95,
            operator: "대구공공시설관리공단",
            courses: ["A", "B", "C", "D"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "울산에서 약 95km · 금호강변 36홀 (A·B·C·D 각 9홀).",
          },
          {
            id: "custom",
            region: "all",
            name: "직접 입력 (다른 파크골프장)",
            location: "원하시는 구장 이름을 직접 적어주세요",
            distanceKm: 0,
            operator: "사용자 자유 설정",
            courses: ["A", "B", "C", "D"],
            defaultPars: {
              A: [...STD_PAR_A],
              B: [...STD_PAR_B],
              C: [...STD_PAR_C],
              D: [...STD_PAR_D],
            },
            note: "어느 구장에서든 A·B·C·D 코스 36홀과 홀별 파(Par)를 자유롭게 설정할 수 있습니다.",
          },
        ];

        function getCourseObj(courseId) {
          return GOLF_COURSES.find((c) => c.id === courseId) || GOLF_COURSES[0];
        }

        function createEmptyScores() {
          return {
            A: new Array(9).fill(0),
            B: new Array(9).fill(0),
            C: new Array(9).fill(0),
            D: new Array(9).fill(0),
          };
        }

        function createInitialState() {
          const coursePars = {};
          GOLF_COURSES.forEach((c) => {
            coursePars[c.id] = {
              A: [...c.defaultPars.A],
              B: [...c.defaultPars.B],
              C: [...c.defaultPars.C],
              D: [...c.defaultPars.D],
            };
          });

          return {
            regionFilter: "all",
            selectedCourseId: "taehwagang",
            customCourseName: "",
            activeViewCourse: "A",
            playerCount: 4,
            soundEnabled: true,
            coursePars,
            players: DEFAULT_NAMES.map((name) => ({
              name,
              scores: createEmptyScores(),
            })),
            activeSignerKey: "rep",
            signatures: {
              rep: null,
              p0: null,
              p1: null,
              p2: null,
              p3: null,
            },
          };
        }

        function loadState() {
          const base = createInitialState();
          try {
            const raw = localStorage.getItem(STORAGE_KEY);
            if (!raw) return base;
            const parsed = JSON.parse(raw);

            if (typeof parsed.regionFilter === "string") {
              base.regionFilter = parsed.regionFilter;
            }
            if (
              typeof parsed.selectedCourseId === "string" &&
              GOLF_COURSES.some((c) => c.id === parsed.selectedCourseId)
            ) {
              base.selectedCourseId = parsed.selectedCourseId;
            }
            if (typeof parsed.customCourseName === "string") {
              base.customCourseName = parsed.customCourseName.slice(0, 24);
            }
            const courseObj = getCourseObj(base.selectedCourseId);
            if (
              parsed.activeViewCourse === "ALL" ||
              (COURSE_KEYS.includes(parsed.activeViewCourse) &&
                courseObj.courses.includes(parsed.activeViewCourse))
            ) {
              base.activeViewCourse = parsed.activeViewCourse;
            } else {
              base.activeViewCourse = courseObj.courses[0];
            }
            if (
              typeof parsed.playerCount === "number" &&
              parsed.playerCount >= 1 &&
              parsed.playerCount <= 4
            ) {
              base.playerCount = parsed.playerCount;
            }
            if (typeof parsed.soundEnabled === "boolean") {
              base.soundEnabled = parsed.soundEnabled;
            }

            if (parsed.coursePars && typeof parsed.coursePars === "object") {
              GOLF_COURSES.forEach((c) => {
                const savedPars = parsed.coursePars[c.id];
                if (savedPars && typeof savedPars === "object") {
                  COURSE_KEYS.forEach((k) => {
                    if (Array.isArray(savedPars[k]) && savedPars[k].length === 9) {
                      base.coursePars[c.id][k] = savedPars[k].map((p) =>
                        p === 3 || p === 4 || p === 5 ? p : 4
                      );
                    }
                  });
                }
              });
            }

            if (Array.isArray(parsed.players) && parsed.players.length === 4) {
              base.players = parsed.players.map((pl, idx) => {
                const sc = createEmptyScores();
                if (pl.scores && typeof pl.scores === "object") {
                  COURSE_KEYS.forEach((k) => {
                    if (Array.isArray(pl.scores[k]) && pl.scores[k].length === 9) {
                      sc[k] = pl.scores[k].map((v) =>
                        typeof v === "number" && v >= 0 && v <= 30 ? Math.floor(v) : 0
                      );
                    }
                  });
                }
                return {
                  name:
                    typeof pl.name === "string" && pl.name.trim() !== ""
                      ? pl.name.slice(0, 12)
                      : DEFAULT_NAMES[idx],
                  scores: sc,
                };
              });
            }

            if (typeof parsed.activeSignerKey === "string") {
              base.activeSignerKey = parsed.activeSignerKey;
            }
            if (parsed.signatures && typeof parsed.signatures === "object") {
              ["rep", "p0", "p1", "p2", "p3"].forEach((key) => {
                if (
                  typeof parsed.signatures[key] === "string" &&
                  parsed.signatures[key].startsWith("data:image/")
                ) {
                  base.signatures[key] = parsed.signatures[key];
                }
              });
            }

            return base;
          } catch (e) {
            return base;
          }
        }

        let state = loadState();
        let audioCtx = null;
        let toastTimer = null;
        let activeKeypadTarget = null;
        const hioTimers = {};

        function persistState() {
          try {
            localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
            return true;
          } catch (e) {
            return false;
          }
        }

        function getAudioContext() {
          if (!state.soundEnabled) return null;
          const AudioContextClass = window.AudioContext || window.webkitAudioContext;
          if (!AudioContextClass) return null;
          if (!audioCtx) audioCtx = new AudioContextClass();
          if (audioCtx.state === "suspended") {
            audioCtx.resume().catch(() => {});
          }
          return audioCtx;
        }

        function playTone(freq, startOffset, duration, type, volume) {
          const ctx = getAudioContext();
          if (!ctx) return;
          const now = ctx.currentTime + startOffset;
          const osc = ctx.createOscillator();
          const gain = ctx.createGain();
          osc.type = type || "sine";
          osc.frequency.setValueAtTime(freq, now);
          gain.gain.setValueAtTime(0.0001, now);
          gain.gain.exponentialRampToValueAtTime(volume || 0.14, now + 0.015);
          gain.gain.exponentialRampToValueAtTime(0.0001, now + duration);
          osc.connect(gain);
          gain.connect(ctx.destination);
          osc.start(now);
          osc.stop(now + duration + 0.02);
        }

        function playStepTap(isPlus) {
          if (!state.soundEnabled) return;
          playTone(isPlus ? 523.25 : 392.0, 0, 0.075, "sine", 0.09);
        }

        function playBirdieChime() {
          if (!state.soundEnabled) return;
          playTone(659.25, 0, 0.14, "triangle", 0.11);
          playTone(880.0, 0.11, 0.22, "triangle", 0.12);
        }

        function playHoleInOneFanfare(forcePlay) {
          if (!state.soundEnabled && !forcePlay) return;
          const AudioContextClass = window.AudioContext || window.webkitAudioContext;
          if (!AudioContextClass) return;
          if (!audioCtx) audioCtx = new AudioContextClass();
          if (audioCtx.state === "suspended") {
            audioCtx.resume().catch(() => {});
          }
          const ctx = audioCtx;
          const notes = [
            { freq: 523.25, time: 0.0, dur: 0.14 },
            { freq: 659.25, time: 0.12, dur: 0.14 },
            { freq: 783.99, time: 0.24, dur: 0.14 },
            { freq: 1046.5, time: 0.36, dur: 0.35 },
            { freq: 783.99, time: 0.56, dur: 0.15 },
            { freq: 1046.5, time: 0.7, dur: 0.55 },
          ];
          notes.forEach((n) => {
            const start = ctx.currentTime + n.time;
            const osc = ctx.createOscillator();
            const overtone = ctx.createOscillator();
            const gain = ctx.createGain();
            const overGain = ctx.createGain();
            osc.type = "triangle";
            osc.frequency.setValueAtTime(n.freq, start);
            overtone.type = "sine";
            overtone.frequency.setValueAtTime(n.freq * 2, start);
            gain.gain.setValueAtTime(0.0001, start);
            gain.gain.exponentialRampToValueAtTime(0.16, start + 0.02);
            gain.gain.exponentialRampToValueAtTime(0.0001, start + n.dur);
            overGain.gain.setValueAtTime(0.05, start);
            overGain.gain.exponentialRampToValueAtTime(0.0001, start + n.dur);
            osc.connect(gain);
            overtone.connect(overGain);
            gain.connect(ctx.destination);
            overGain.connect(ctx.destination);
            osc.start(start);
            overtone.start(start);
            osc.stop(start + n.dur + 0.03);
            overtone.stop(start + n.dur + 0.03);
          });
        }

        function getActiveGolfCourseDisplayName() {
          const obj = getCourseObj(state.selectedCourseId);
          if (obj.id === "custom") {
            return state.customCourseName.trim() || "직접 입력 파크골프장";
          }
          return obj.name;
        }

        function getCurrentCoursePars(courseKey) {
          const parsByCourse = state.coursePars[state.selectedCourseId];
          if (parsByCourse && parsByCourse[courseKey]) {
            return parsByCourse[courseKey];
          }
          return [...STD_PAR_A];
        }

        function renderTodayDate() {
          const now = new Date();
          const days = ["일요일", "월요일", "화요일", "수요일", "목요일", "금요일", "토요일"];
          document.getElementById("todayDateText").textContent =
            `${now.getFullYear()}년 ${now.getMonth() + 1}월 ${now.getDate()}일 ${days[now.getDay()]}`;
        }

        function getShortScoreEvaluation(strokes, par) {
          if (strokes <= 0) return { label: "", tagClass: "", cellClass: "" };
          if (strokes === 1) return { label: "홀인원!", tagClass: "tag-hio", cellClass: "is-hio" };
          const diff = strokes - par;
          if (diff <= -3) return { label: `알바(${diff})`, tagClass: "tag-under", cellClass: "is-under" };
          if (diff === -2) return { label: "이글(-2)", tagClass: "tag-under", cellClass: "is-under" };
          if (diff === -1) return { label: "버디(-1)", tagClass: "tag-under", cellClass: "is-under" };
          if (diff === 0) return { label: "파(E)", tagClass: "tag-even", cellClass: "" };
          if (diff === 1) return { label: "보기(+1)", tagClass: "tag-over", cellClass: "is-over" };
          if (diff === 2) return { label: "더블(+2)", tagClass: "tag-over", cellClass: "is-over" };
          return { label: `+${diff}`, tagClass: "tag-over", cellClass: "is-over" };
        }

        function formatParDiffText(diff, completedHoles) {
          if (completedHoles === 0) return { text: "대기", className: "diff-even" };
          if (diff < 0) return { text: `${diff} 언더`, className: "diff-under" };
          if (diff === 0) return { text: "이븐 (E)", className: "diff-even" };
          return { text: `+${diff} 오버`, className: "diff-over" };
        }

        function getPlayerDisplayName(index) {
          const name = state.players[index].name.trim();
          return name || DEFAULT_NAMES[index];
        }

        function showToast(message) {
          const toast = document.getElementById("toastBanner");
          toast.textContent = message;
          toast.classList.add("visible");
          if (toastTimer) clearTimeout(toastTimer);
          toastTimer = setTimeout(() => {
            toast.classList.remove("visible");
          }, 2800);
        }

        function openHoleInOneModal(playerName, courseKey, holeNumber) {
          const modal = document.getElementById("holeInOneModal");
          document.getElementById("hioModalDesc").textContent =
            `${playerName} 님이 ${courseKey}코스 ${holeNumber}번 홀에서 환상적인 홀인원(1타)을 기록하셨습니다!`;
          modal.classList.add("open");
          document.getElementById("hioCloseBtn").focus();
        }

        function renderHeader() {
          const courseObj = getCourseObj(state.selectedCourseId);
          const totalHoles = courseObj.courses.length * 9;
          let totalPar = 0;
          courseObj.courses.forEach((k) => {
            totalPar += getCurrentCoursePars(k).reduce((a, b) => a + b, 0);
          });

          document.getElementById("headerCourseText").textContent =
            getActiveGolfCourseDisplayName();
          document.getElementById("courseSummaryText").textContent =
            `${courseObj.courses.join("·")}코스 (${totalHoles}홀 · 기준 파 ${totalPar})`;

          const soundBtn = document.getElementById("soundToggleBtn");
          soundBtn.setAttribute("aria-pressed", String(state.soundEnabled));
          document.getElementById("soundIcon").textContent = state.soundEnabled ? "🔊" : "🔇";
          document.getElementById("soundLabel").textContent = state.soundEnabled
            ? "효과음 켜짐"
            : "효과음 꺼짐";
        }

        function renderCourseSelector() {
          document.querySelectorAll(".region-btn").forEach((btn) => {
            btn.classList.toggle("active", btn.dataset.region === state.regionFilter);
          });

          const select = document.getElementById("courseSelect");
          select.innerHTML = "";

          const filtered = GOLF_COURSES.filter((c) => {
            if (state.regionFilter === "all") return true;
            return c.region === state.regionFilter || c.id === "custom";
          });

          const hasSelected = filtered.some((c) => c.id === state.selectedCourseId);
          const listToShow = hasSelected
            ? filtered
            : [getCourseObj(state.selectedCourseId), ...filtered];

          listToShow.forEach((c) => {
            const opt = document.createElement("option");
            opt.value = c.id;
            const totalHoles = c.courses.length * 9;
            if (c.id === "custom") {
              opt.textContent = `[직접 설정] ${c.name} (A·B·C·D 36홀)`;
            } else {
              const distLabel = c.distanceKm <= 25 ? "울산" : `약 ${c.distanceKm}km`;
              opt.textContent = `[${distLabel}] ${c.name} (${totalHoles}홀 · ${c.courses.join("·")})`;
            }
            if (c.id === state.selectedCourseId) opt.selected = true;
            select.appendChild(opt);
          });

          const currentCourse = getCourseObj(state.selectedCourseId);
          const customRow = document.getElementById("customCourseRow");
          customRow.classList.toggle("visible", currentCourse.id === "custom");
          const customInput = document.getElementById("customCourseInput");
          if (document.activeElement !== customInput) {
            customInput.value = state.customCourseName;
          }

          document.getElementById("selectedCourseName").textContent =
            getActiveGolfCourseDisplayName();
          document.getElementById("selectedCourseDistance").textContent =
            currentCourse.id === "custom"
              ? "사용자 지정 코스"
              : currentCourse.distanceKm <= 25
                ? `울산 관내 (${currentCourse.distanceKm}km)`
                : `울산 기준 약 ${currentCourse.distanceKm}km`;

          document.getElementById("selectedCourseMeta").textContent =
            `${currentCourse.location} · 운영: ${currentCourse.operator}`;
          document.getElementById("selectedCourseNote").textContent = currentCourse.note;
        }

        function computeLeaderboard() {
          const courseObj = getCourseObj(state.selectedCourseId);
          const availableCourses = courseObj.courses;
          const totalHolesAvailable = availableCourses.length * 9;
          const rows = [];

          for (let p = 0; p < state.playerCount; p++) {
            const courseTotals = { A: 0, B: 0, C: 0, D: 0 };
            const coursePlayedCount = { A: 0, B: 0, C: 0, D: 0 };
            const coursePlayedPar = { A: 0, B: 0, C: 0, D: 0 };
            let totalStrokes = 0;
            let playedPar = 0;
            let completedHoles = 0;

            availableCourses.forEach((cKey) => {
              const pars = getCurrentCoursePars(cKey);
              for (let h = 0; h < 9; h++) {
                const s = state.players[p].scores[cKey][h];
                if (s > 0) {
                  courseTotals[cKey] += s;
                  coursePlayedCount[cKey] += 1;
                  coursePlayedPar[cKey] += pars[h];
                  totalStrokes += s;
                  playedPar += pars[h];
                  completedHoles += 1;
                }
              }
            });

            rows.push({
              index: p,
              name: getPlayerDisplayName(p),
              courseTotals,
              coursePlayedCount,
              coursePlayedPar,
              totalStrokes,
              playedPar,
              completedHoles,
              totalHolesAvailable,
              diff: totalStrokes - playedPar,
            });
          }

          const sorted = [...rows].sort((a, b) => {
            if (a.completedHoles === 0 && b.completedHoles === 0) return a.index - b.index;
            if (a.completedHoles === 0) return 1;
            if (b.completedHoles === 0) return -1;
            if (a.totalStrokes !== b.totalStrokes) return a.totalStrokes - b.totalStrokes;
            if (a.diff !== b.diff) return a.diff - b.diff;
            return a.index - b.index;
          });

          const rankByPlayerIndex = {};
          let currentRank = 1;
          for (let i = 0; i < sorted.length; i++) {
            if (sorted[i].completedHoles === 0) {
              sorted[i].rank = null;
            } else if (
              i > 0 &&
              sorted[i - 1].completedHoles > 0 &&
              sorted[i].totalStrokes === sorted[i - 1].totalStrokes &&
              sorted[i].diff === sorted[i - 1].diff
            ) {
              sorted[i].rank = sorted[i - 1].rank;
            } else {
              sorted[i].rank = currentRank;
            }
            rankByPlayerIndex[sorted[i].index] = sorted[i].rank;
            currentRank++;
          }

          return { byPlayer: rows, sorted, rankByPlayerIndex };
        }

        function renderScorecardMatrix() {
          const courseObj = getCourseObj(state.selectedCourseId);
          if (
            state.activeViewCourse !== "ALL" &&
            !courseObj.courses.includes(state.activeViewCourse)
          ) {
            state.activeViewCourse = courseObj.courses[0];
          }

          document.querySelectorAll(".count-btn").forEach((btn) => {
            btn.classList.toggle("active", Number(btn.dataset.count) === state.playerCount);
          });

          const tabsBar = document.getElementById("courseTabsBar");
          tabsBar.innerHTML = "";

          courseObj.courses.forEach((cKey) => {
            const pars = getCurrentCoursePars(cKey);
            const parSum = pars.reduce((a, b) => a + b, 0);
            const btn = document.createElement("button");
            btn.type = "button";
            btn.className =
              "course-tab-btn" + (state.activeViewCourse === cKey ? " active" : "");
            btn.textContent = `${cKey}코스 (파${parSum})`;
            btn.addEventListener("click", () => {
              state.activeViewCourse = cKey;
              persistState();
              renderScorecardMatrix();
            });
            tabsBar.appendChild(btn);
          });

          const allBtn = document.createElement("button");
          allBtn.type = "button";
          allBtn.className =
            "course-tab-btn" + (state.activeViewCourse === "ALL" ? " active" : "");
          allBtn.textContent = `전체 (${courseObj.courses.join("·")}) 보기`;
          allBtn.addEventListener("click", () => {
            state.activeViewCourse = "ALL";
            persistState();
            renderScorecardMatrix();
          });
          tabsBar.appendChild(allBtn);

          const standings = computeLeaderboard();
          const table = document.getElementById("scorecardMatrixTable");
          table.innerHTML = "";

          const thead = document.createElement("thead");
          thead.className = "matrix-thead";
          const headTr = document.createElement("tr");

          const holeTh = document.createElement("th");
          holeTh.className = "col-hole";
          holeTh.textContent = "홀 · 파";
          headTr.appendChild(holeTh);

          for (let p = 0; p < state.playerCount; p++) {
            const th = document.createElement("th");
            const wrap = document.createElement("div");
            wrap.className = "player-col-header";

            const badge = document.createElement("span");
            badge.className = "player-cap-badge";
            const dot = document.createElement("span");
            dot.className = `cap-dot cap-${p}`;
            dot.setAttribute("aria-hidden", "true");
            const txt = document.createElement("span");
            txt.textContent = `${p + 1}번 선수`;
            badge.appendChild(dot);
            badge.appendChild(txt);

            const input = document.createElement("input");
            input.type = "text";
            input.className = "player-header-input";
            input.maxLength = 10;
            input.value = state.players[p].name;
            input.placeholder = DEFAULT_NAMES[p];
            input.setAttribute("aria-label", `${p + 1}번 선수 이름 입력`);

            input.addEventListener("input", (e) => {
              state.players[p].name = e.target.value;
              persistState();
              renderLeaderboard();
              renderSignArea();
            });

            wrap.appendChild(badge);
            wrap.appendChild(input);
            th.appendChild(wrap);
            headTr.appendChild(th);
          }

          thead.appendChild(headTr);
          table.appendChild(thead);

          const tbody = document.createElement("tbody");
          const coursesToRender =
            state.activeViewCourse === "ALL"
              ? courseObj.courses
              : [state.activeViewCourse];

          coursesToRender.forEach((cKey) => {
            const pars = getCurrentCoursePars(cKey);
            let courseParSum = 0;

            for (let h = 0; h < 9; h++) {
              const parVal = pars[h];
              courseParSum += parVal;

              const tr = document.createElement("tr");

              const holeTd = document.createElement("td");
              holeTd.className = "col-hole hole-cell";

              const inner = document.createElement("div");
              inner.className = "hole-cell-inner";

              const nameGrp = document.createElement("div");
              nameGrp.className = "hole-name-group";

              const mark = document.createElement("span");
              mark.className = `course-letter-mark mark-${cKey}`;
              mark.textContent = cKey;

              const holeTxt = document.createElement("span");
              holeTxt.className = "hole-num-label";
              holeTxt.textContent = `${h + 1}번`;

              nameGrp.appendChild(mark);
              nameGrp.appendChild(holeTxt);

              const parBtn = document.createElement("button");
              parBtn.type = "button";
              parBtn.className = `par-cycle-btn par-${parVal}`;
              parBtn.textContent = `파${parVal}`;
              parBtn.title = "누르면 파3 → 파4 → 파5 순서로 바뀝니다";
              parBtn.setAttribute(
                "aria-label",
                `${cKey}코스 ${h + 1}번 홀 기준타수 파${parVal}. 누르면 변경됩니다.`
              );
              parBtn.addEventListener("click", () => {
                const nextPar = parVal === 3 ? 4 : parVal === 4 ? 5 : 3;
                state.coursePars[state.selectedCourseId][cKey][h] = nextPar;
                persistState();
                playStepTap(true);
                renderHeader();
                renderScorecardMatrix();
                renderLeaderboard();
                showToast(`${cKey}코스 ${h + 1}번 홀을 파${nextPar}로 변경했습니다.`);
              });

              inner.appendChild(nameGrp);
              inner.appendChild(parBtn);
              holeTd.appendChild(inner);
              tr.appendChild(holeTd);

              for (let p = 0; p < state.playerCount; p++) {
                const strokes = state.players[p].scores[cKey][h];
                const evalInfo = getShortScoreEvaluation(strokes, parVal);

                const td = document.createElement("td");
                td.className = "score-cell";
                if (evalInfo.cellClass) td.classList.add(evalInfo.cellClass);
                if (
                  activeKeypadTarget &&
                  activeKeypadTarget.playerIndex === p &&
                  activeKeypadTarget.courseKey === cKey &&
                  activeKeypadTarget.holeIndex === h
                ) {
                  td.classList.add("is-active-target");
                }

                const stepper = document.createElement("div");
                stepper.className = "cell-stepper";

                const minusBtn = document.createElement("button");
                minusBtn.type = "button";
                minusBtn.className = "cell-step-btn cell-step-minus";
                minusBtn.textContent = "−";
                minusBtn.disabled = strokes <= 0;
                minusBtn.setAttribute(
                  "aria-label",
                  `${getPlayerDisplayName(p)} ${cKey} ${h + 1}번 홀 1타 줄이기`
                );
                minusBtn.addEventListener("click", () => {
                  updatePlayerScore(p, cKey, h, -1);
                });

                const scoreTrigger = document.createElement("button");
                scoreTrigger.type = "button";
                scoreTrigger.className = "cell-score-trigger";
                scoreTrigger.setAttribute(
                  "aria-label",
                  `${getPlayerDisplayName(p)} ${cKey} ${h + 1}번 홀 타수 입력 (${strokes > 0 ? strokes + "타" : "미입력"})`
                );
                scoreTrigger.addEventListener("click", () => {
                  openScoreKeypad(p, cKey, h);
                });

                const numSpan = document.createElement("span");
                numSpan.className =
                  "cell-score-num" + (strokes === 0 ? " is-empty" : "");
                numSpan.textContent = strokes > 0 ? String(strokes) : "-";

                scoreTrigger.appendChild(numSpan);

                if (evalInfo.label) {
                  const tagSpan = document.createElement("span");
                  tagSpan.className = `cell-score-tag ${evalInfo.tagClass}`;
                  tagSpan.textContent = evalInfo.label;
                  scoreTrigger.appendChild(tagSpan);
                }

                const plusBtn = document.createElement("button");
                plusBtn.type = "button";
                plusBtn.className = "cell-step-btn cell-step-plus";
                plusBtn.textContent = "+";
                plusBtn.setAttribute(
                  "aria-label",
                  `${getPlayerDisplayName(p)} ${cKey} ${h + 1}번 홀 1타 늘리기`
                );
                plusBtn.addEventListener("click", () => {
                  updatePlayerScore(p, cKey, h, 1);
                });

                stepper.appendChild(minusBtn);
                stepper.appendChild(scoreTrigger);
                stepper.appendChild(plusBtn);
                td.appendChild(stepper);
                tr.appendChild(td);
              }

              tbody.appendChild(tr);
            }

            const subTr = document.createElement("tr");
            subTr.className = "subtotal-row";

            const subHoleTd = document.createElement("td");
            subHoleTd.className = "col-hole hole-cell";
            subHoleTd.textContent = `${cKey}코스 합계 (파${courseParSum})`;
            subTr.appendChild(subHoleTd);

            for (let p = 0; p < state.playerCount; p++) {
              const pInfo = standings.byPlayer[p];
              const cTotal = pInfo.courseTotals[cKey];
              const cPlayed = pInfo.coursePlayedCount[cKey];
              const cDiff = cTotal - pInfo.coursePlayedPar[cKey];

              const td = document.createElement("td");
              if (cPlayed === 0) {
                td.textContent = "-";
              } else {
                const diffInfo = formatParDiffText(cDiff, cPlayed);
                const mainDiv = document.createElement("div");
                mainDiv.className = "sum-main-num";
                mainDiv.textContent = `${cTotal}타`;
                const subDiv = document.createElement("div");
                subDiv.className = `sum-sub-diff ${diffInfo.className}`;
                subDiv.textContent = `${diffInfo.text} (${cPlayed}/9)`;
                td.appendChild(mainDiv);
                td.appendChild(subDiv);
              }
              subTr.appendChild(td);
            }
            tbody.appendChild(subTr);
          });

          let totalCourseParAll = 0;
          courseObj.courses.forEach((k) => {
            totalCourseParAll += getCurrentCoursePars(k).reduce((a, b) => a + b, 0);
          });

          const grandTr = document.createElement("tr");
          grandTr.className = "grandtotal-row";

          const grandHoleTd = document.createElement("td");
          grandHoleTd.className = "col-hole hole-cell";
          grandHoleTd.textContent = `총합계 (${courseObj.courses.join("+")} · 파${totalCourseParAll})`;
          grandTr.appendChild(grandHoleTd);

          for (let p = 0; p < state.playerCount; p++) {
            const pInfo = standings.byPlayer[p];
            const td = document.createElement("td");
            if (pInfo.completedHoles === 0) {
              td.textContent = "-";
            } else {
              const diffStr = formatParDiffText(pInfo.diff, pInfo.completedHoles).text;
              const mainDiv = document.createElement("div");
              mainDiv.className = "sum-main-num";
              mainDiv.textContent = `${pInfo.totalStrokes}타`;
              const subDiv = document.createElement("div");
              subDiv.className = "sum-sub-diff";
              subDiv.textContent = `${diffStr} (${pInfo.completedHoles}/${pInfo.totalHolesAvailable})`;
              td.appendChild(mainDiv);
              td.appendChild(subDiv);
            }
            grandTr.appendChild(td);
          }
          tbody.appendChild(grandTr);

          const rankTr = document.createElement("tr");
          rankTr.className = "rank-summary-row";

          const rankHoleTd = document.createElement("td");
          rankHoleTd.className = "col-hole hole-cell";
          rankHoleTd.textContent = "현재 순위";
          rankTr.appendChild(rankHoleTd);

          for (let p = 0; p < state.playerCount; p++) {
            const rank = standings.rankByPlayerIndex[p];
            const td = document.createElement("td");
            td.textContent = rank ? `${rank}등` : "대기";
            rankTr.appendChild(td);
          }
          tbody.appendChild(rankTr);

          table.appendChild(tbody);
        }

        function renderLeaderboard() {
          const courseObj = getCourseObj(state.selectedCourseId);
          const list = document.getElementById("leaderboardList");
          list.innerHTML = "";
          const { sorted } = computeLeaderboard();

          sorted.forEach((item) => {
            const row = document.createElement("div");
            row.className = "rank-row" + (item.rank === 1 ? " rank-first" : "");

            const posEl = document.createElement("div");
            posEl.className = "rank-position";
            if (item.rank === 1) posEl.textContent = "🏆 1등";
            else if (item.rank === 2) posEl.textContent = "🥈 2등";
            else if (item.rank === 3) posEl.textContent = "🥉 3등";
            else if (item.rank === 4) posEl.textContent = "4등";
            else posEl.textContent = "대기";

            const metaEl = document.createElement("div");
            metaEl.className = "rank-player-meta";

            const nameEl = document.createElement("div");
            nameEl.className = "rank-player-name";
            nameEl.textContent = item.name;

            const breakdownEl = document.createElement("div");
            breakdownEl.className = "rank-course-breakdown";
            breakdownEl.textContent = courseObj.courses
              .map((k) => `${k}: ${item.courseTotals[k] > 0 ? item.courseTotals[k] : "-"}`)
              .join(" · ");

            const holesEl = document.createElement("div");
            holesEl.className = "rank-holes-played";
            holesEl.textContent = `${item.completedHoles}/${item.totalHolesAvailable}홀 완료`;

            metaEl.appendChild(nameEl);
            metaEl.appendChild(breakdownEl);
            metaEl.appendChild(holesEl);

            const scoreSummary = document.createElement("div");
            scoreSummary.className = "rank-score-summary";

            const totalEl = document.createElement("div");
            totalEl.className = "rank-total-strokes";
            totalEl.textContent = item.completedHoles > 0 ? `${item.totalStrokes}타` : "-타";

            const diffInfo = formatParDiffText(item.diff, item.completedHoles);
            const diffEl = document.createElement("div");
            diffEl.className = `rank-par-diff ${diffInfo.className}`;
            diffEl.textContent = diffInfo.text;

            scoreSummary.appendChild(totalEl);
            scoreSummary.appendChild(diffEl);

            row.appendChild(posEl);
            row.appendChild(metaEl);
            row.appendChild(scoreSummary);
            list.appendChild(row);
          });
        }

        function openScoreKeypad(playerIndex, courseKey, holeIndex) {
          activeKeypadTarget = { playerIndex, courseKey, holeIndex };
          renderKeypadContent();
          document.getElementById("scoreEntrySheet").classList.add("open");
          renderScorecardMatrix();
        }

        function closeScoreKeypad() {
          activeKeypadTarget = null;
          document.getElementById("scoreEntrySheet").classList.remove("open");
          renderScorecardMatrix();
        }

        function renderKeypadContent() {
          if (!activeKeypadTarget) return;
          const { playerIndex, courseKey, holeIndex } = activeKeypadTarget;
          const par = getCurrentCoursePars(courseKey)[holeIndex];
          const strokes = state.players[playerIndex].scores[courseKey][holeIndex];
          const pName = getPlayerDisplayName(playerIndex);

          document.getElementById("keypadTitle").textContent =
            `${courseKey}코스 ${holeIndex + 1}번 홀 (파${par}) · ${pName}`;
          document.getElementById("keypadBigNum").textContent = String(strokes);

          const evalInfo = getShortScoreEvaluation(strokes, par);
          document.getElementById("keypadEvalText").textContent =
            strokes === 0 ? "아직 입력 전" : evalInfo.label;
          document.getElementById("keypadMinusBtn").disabled = strokes <= 0;

          const quickGrid = document.getElementById("keypadQuickGrid");
          quickGrid.innerHTML = "";
          for (let n = 1; n <= 8; n++) {
            const btn = document.createElement("button");
            btn.type = "button";
            btn.className = "quick-num-btn" + (strokes === n ? " active" : "");

            const numSpan = document.createElement("span");
            numSpan.textContent = String(n);

            const subSpan = document.createElement("span");
            subSpan.className = "quick-num-sub";
            const ev = getShortScoreEvaluation(n, par);
            subSpan.textContent = ev.label || `${n}타`;

            btn.appendChild(numSpan);
            btn.appendChild(subSpan);
            btn.addEventListener("click", () => {
              setPlayerScoreExact(playerIndex, courseKey, holeIndex, n);
            });
            quickGrid.appendChild(btn);
          }
        }

        function setPlayerScoreExact(playerIndex, courseKey, holeIndex, targetScore) {
          const next = Math.max(0, Math.min(30, targetScore));
          const prev = state.players[playerIndex].scores[courseKey][holeIndex];
          state.players[playerIndex].scores[courseKey][holeIndex] = next;
          persistState();

          const timerKey = `${playerIndex}_${courseKey}_${holeIndex}`;
          if (hioTimers[timerKey]) {
            clearTimeout(hioTimers[timerKey]);
            delete hioTimers[timerKey];
          }

          const holePar = getCurrentCoursePars(courseKey)[holeIndex];
          if (next === 1) {
            playHoleInOneFanfare(false);
            openHoleInOneModal(getPlayerDisplayName(playerIndex), courseKey, holeIndex + 1);
          } else if (next > 1 && next < holePar) {
            playBirdieChime();
          } else if (next !== prev) {
            playStepTap(next > prev);
          }

          renderScorecardMatrix();
          renderLeaderboard();
          renderKeypadContent();
        }

        function updatePlayerScore(playerIndex, courseKey, holeIndex, delta) {
          const prev = state.players[playerIndex].scores[courseKey][holeIndex];
          const next = Math.max(0, Math.min(30, prev + delta));
          if (prev === next) return;

          state.players[playerIndex].scores[courseKey][holeIndex] = next;
          persistState();

          const timerKey = `${playerIndex}_${courseKey}_${holeIndex}`;
          if (hioTimers[timerKey]) {
            clearTimeout(hioTimers[timerKey]);
            delete hioTimers[timerKey];
          }

          const holePar = getCurrentCoursePars(courseKey)[holeIndex];

          if (next === 1) {
            playStepTap(delta > 0);
            hioTimers[timerKey] = setTimeout(() => {
              delete hioTimers[timerKey];
              if (state.players[playerIndex].scores[courseKey][holeIndex] === 1) {
                playHoleInOneFanfare(false);
                openHoleInOneModal(
                  getPlayerDisplayName(playerIndex),
                  courseKey,
                  holeIndex + 1
                );
              }
            }, 450);
          } else if (next > 1 && next < holePar && delta < 0) {
            playBirdieChime();
          } else {
            playStepTap(delta > 0);
          }

          renderScorecardMatrix();
          renderLeaderboard();
          renderKeypadContent();
        }

        /* 서명 패드 */
        const sigCanvas = document.getElementById("signatureCanvas");
        const sigCtx = sigCanvas.getContext("2d");
        let isDrawingSig = false;
        let lastSigPt = null;

        function getSignerOptions() {
          const opts = [{ key: "rep", label: "대표 확인자" }];
          for (let i = 0; i < state.playerCount; i++) {
            opts.push({ key: `p${i}`, label: getPlayerDisplayName(i) });
          }
          return opts;
        }

        function resizeAndLoadSignatureCanvas() {
          const rect = sigCanvas.getBoundingClientRect();
          if (rect.width === 0 || rect.height === 0) return;
          const dpr = window.devicePixelRatio || 1;
          sigCanvas.width = Math.round(rect.width * dpr);
          sigCanvas.height = Math.round(rect.height * dpr);
          sigCtx.setTransform(dpr, 0, 0, dpr, 0, 0);
          sigCtx.lineCap = "round";
          sigCtx.lineJoin = "round";
          sigCtx.lineWidth = 3.5;
          sigCtx.strokeStyle = "#17271d";

          sigCtx.clearRect(0, 0, rect.width, rect.height);
          const dataUrl = state.signatures[state.activeSignerKey];
          const placeholder = document.getElementById("signaturePlaceholder");

          if (dataUrl) {
            placeholder.classList.add("hidden");
            const img = new Image();
            img.onload = () => {
              sigCtx.clearRect(0, 0, rect.width, rect.height);
              sigCtx.drawImage(img, 0, 0, rect.width, rect.height);
            };
            img.src = dataUrl;
          } else {
            placeholder.classList.remove("hidden");
          }
        }

        function renderSignArea() {
          const signers = getSignerOptions();
          if (!signers.some((s) => s.key === state.activeSignerKey)) {
            state.activeSignerKey = "rep";
          }

          const tabsEl = document.getElementById("signerTabs");
          tabsEl.innerHTML = "";
          signers.forEach((s) => {
            const btn = document.createElement("button");
            btn.type = "button";
            const isSigned = Boolean(state.signatures[s.key]);
            btn.className =
              "signer-tab-btn" +
              (isSigned ? " signed" : "") +
              (state.activeSignerKey === s.key ? " active" : "");
            btn.textContent = isSigned ? `${s.label} (완료)` : s.label;
            btn.addEventListener("click", () => {
              state.activeSignerKey = s.key;
              persistState();
              renderSignArea();
            });
            tabsEl.appendChild(btn);
          });

          const activeOpt = signers.find((s) => s.key === state.activeSignerKey);
          const hasSig = Boolean(state.signatures[state.activeSignerKey]);
          document.getElementById("signStatusText").textContent = hasSig
            ? `${activeOpt.label} 서명이 저장되었습니다.`
            : `${activeOpt.label} 서명 대기 중`;

          const gallery = document.getElementById("savedSignaturesGallery");
          gallery.innerHTML = "";
          signers.forEach((s) => {
            const card = document.createElement("div");
            card.className = "saved-sign-card";

            const lbl = document.createElement("div");
            lbl.className = "saved-sign-label";
            lbl.textContent = s.label;

            const prev = document.createElement("div");
            prev.className = "saved-sign-preview";
            if (state.signatures[s.key]) {
              const img = document.createElement("img");
              img.src = state.signatures[s.key];
              img.alt = `${s.label} 서명`;
              prev.appendChild(img);
            } else {
              prev.textContent = "미서명";
            }

            card.appendChild(lbl);
            card.appendChild(prev);
            gallery.appendChild(card);
          });

          resizeAndLoadSignatureCanvas();
        }

        function getCanvasPoint(e) {
          const rect = sigCanvas.getBoundingClientRect();
          return { x: e.clientX - rect.left, y: e.clientY - rect.top };
        }

        sigCanvas.addEventListener("pointerdown", (e) => {
          e.preventDefault();
          sigCanvas.setPointerCapture(e.pointerId);
          isDrawingSig = true;
          lastSigPt = getCanvasPoint(e);
          document.getElementById("signaturePlaceholder").classList.add("hidden");
          sigCtx.beginPath();
          sigCtx.arc(lastSigPt.x, lastSigPt.y, 1.8, 0, Math.PI * 2);
          sigCtx.fillStyle = "#17271d";
          sigCtx.fill();
        });

        sigCanvas.addEventListener("pointermove", (e) => {
          if (!isDrawingSig || !lastSigPt) return;
          e.preventDefault();
          const pt = getCanvasPoint(e);
          sigCtx.beginPath();
          sigCtx.moveTo(lastSigPt.x, lastSigPt.y);
          sigCtx.lineTo(pt.x, pt.y);
          sigCtx.stroke();
          lastSigPt = pt;
        });

        function finishSignatureStroke() {
          if (!isDrawingSig) return;
          isDrawingSig = false;
          lastSigPt = null;
          state.signatures[state.activeSignerKey] = sigCanvas.toDataURL("image/png");
          persistState();
          renderSignArea();
        }

        sigCanvas.addEventListener("pointerup", finishSignatureStroke);
        sigCanvas.addEventListener("pointercancel", finishSignatureStroke);

        function renderAll() {
          renderHeader();
          renderCourseSelector();
          renderScorecardMatrix();
          renderLeaderboard();
          renderSignArea();
        }

        function buildShareText() {
          const now = new Date();
          const days = ["일", "월", "화", "수", "목", "금", "토"];
          const dateStr = `${now.getFullYear()}.${now.getMonth() + 1}.${now.getDate()}(${days[now.getDay()]})`;
          const courseObj = getCourseObj(state.selectedCourseId);
          const courseName = getActiveGolfCourseDisplayName();

          let totalCoursePar = 0;
          courseObj.courses.forEach((k) => {
            totalCoursePar += getCurrentCoursePars(k).reduce((a, b) => a + b, 0);
          });

          const { sorted } = computeLeaderboard();
          const lines = [
            `⛳ 즐거운 파크골프 스코어 카드`,
            `📍 구장: ${courseName}`,
            `📅 ${dateStr} · ${courseObj.courses.join("·")}코스 (기준 파 ${totalCoursePar})`,
            "",
            "🏆 최종 순위 및 코스별 합계",
          ];

          sorted.forEach((item) => {
            const rankStr = item.rank ? `${item.rank}등` : "대기";
            if (item.completedHoles === 0) {
              lines.push(`${rankStr}. ${item.name} : 기록 없음`);
            } else {
              const diffStr = formatParDiffText(item.diff, item.completedHoles).text;
              const abcdStr = courseObj.courses
                .map((k) => `${k}:${item.courseTotals[k] > 0 ? item.courseTotals[k] : "-"}`)
                .join(" ");
              lines.push(
                `${rankStr}. ${item.name} : 총 ${item.totalStrokes}타 (${diffStr}) [${abcdStr}]`
              );
            }
          });

          const signedLabels = getSignerOptions()
            .filter((s) => Boolean(state.signatures[s.key]))
            .map((s) => s.label);
          if (signedLabels.length > 0) {
            lines.push("", `✍️ 확인 서명 완료: ${signedLabels.join(", ")}`);
          }

          lines.push("", "📋 코스·홀별 타수");
          courseObj.courses.forEach((k) => {
            const pars = getCurrentCoursePars(k);
            let hasAny = false;
            for (let p = 0; p < state.playerCount; p++) {
              if (state.players[p].scores[k].some((v) => v > 0)) {
                hasAny = true;
                break;
              }
            }
            if (!hasAny) return;
            lines.push(`[${k}코스]`);
            for (let h = 0; h < 9; h++) {
              const holeScores = [];
              for (let p = 0; p < state.playerCount; p++) {
                const s = state.players[p].scores[k][h];
                holeScores.push(`${getPlayerDisplayName(p)} ${s > 0 ? s : "-"}`);
              }
              lines.push(`${k} ${h + 1}번(파${pars[h]}): ${holeScores.join(" / ")}`);
            }
          });

          return lines.join("\n");
        }

        async function copyTextToClipboard(text) {
          if (navigator.clipboard && window.isSecureContext) {
            try {
              await navigator.clipboard.writeText(text);
              return true;
            } catch (e) {}
          }
          try {
            const textarea = document.createElement("textarea");
            textarea.value = text;
            textarea.style.position = "fixed";
            textarea.style.top = "-9999px";
            textarea.style.left = "-9999px";
            document.body.appendChild(textarea);
            textarea.focus();
            textarea.select();
            const ok = document.execCommand("copy");
            document.body.removeChild(textarea);
            return ok;
          } catch (e) {
            return false;
          }
        }

        function bindEvents() {
          window.addEventListener("resize", () => {
            resizeAndLoadSignatureCanvas();
          });

          document.getElementById("soundToggleBtn").addEventListener("click", () => {
            state.soundEnabled = !state.soundEnabled;
            persistState();
            renderHeader();
            if (state.soundEnabled) {
              playStepTap(true);
              showToast("효과음이 켜졌습니다.");
            } else {
              showToast("효과음이 꺼졌습니다.");
            }
          });

          document.querySelectorAll(".region-btn").forEach((btn) => {
            btn.addEventListener("click", () => {
              state.regionFilter = btn.dataset.region;
              persistState();
              renderCourseSelector();
            });
          });

          document.getElementById("courseSelect").addEventListener("change", (e) => {
            state.selectedCourseId = e.target.value;
            const courseObj = getCourseObj(state.selectedCourseId);
            if (
              state.activeViewCourse !== "ALL" &&
              !courseObj.courses.includes(state.activeViewCourse)
            ) {
              state.activeViewCourse = courseObj.courses[0];
            }
            persistState();
            playStepTap(true);
            renderAll();
            showToast(`${getActiveGolfCourseDisplayName()} 코스가 선택되었습니다.`);
          });

          document.getElementById("customCourseInput").addEventListener("input", (e) => {
            state.customCourseName = e.target.value;
            persistState();
            renderHeader();
            document.getElementById("selectedCourseName").textContent =
              getActiveGolfCourseDisplayName();
          });

          document.querySelectorAll(".count-btn").forEach((btn) => {
            btn.addEventListener("click", () => {
              state.playerCount = Number(btn.dataset.count);
              persistState();
              renderScorecardMatrix();
              renderLeaderboard();
              renderSignArea();
            });
          });

          document.getElementById("keypadCloseBtn").addEventListener("click", closeScoreKeypad);
          document.getElementById("scoreEntrySheet").addEventListener("click", (e) => {
            if (e.target.id === "scoreEntrySheet") closeScoreKeypad();
          });
          document.getElementById("keypadMinusBtn").addEventListener("click", () => {
            if (!activeKeypadTarget) return;
            updatePlayerScore(
              activeKeypadTarget.playerIndex,
              activeKeypadTarget.courseKey,
              activeKeypadTarget.holeIndex,
              -1
            );
          });
          document.getElementById("keypadPlusBtn").addEventListener("click", () => {
            if (!activeKeypadTarget) return;
            updatePlayerScore(
              activeKeypadTarget.playerIndex,
              activeKeypadTarget.courseKey,
              activeKeypadTarget.holeIndex,
              1
            );
          });
          document.getElementById("keypadNextPlayerBtn").addEventListener("click", () => {
            if (!activeKeypadTarget) return;
            const nextP = (activeKeypadTarget.playerIndex + 1) % state.playerCount;
            openScoreKeypad(
              nextP,
              activeKeypadTarget.courseKey,
              activeKeypadTarget.holeIndex
            );
          });
          document.getElementById("keypadNextHoleBtn").addEventListener("click", () => {
            if (!activeKeypadTarget) return;
            const courseObj = getCourseObj(state.selectedCourseId);
            let nextH = activeKeypadTarget.holeIndex + 1;
            let nextC = activeKeypadTarget.courseKey;
            if (nextH >= 9) {
              const cIdx = courseObj.courses.indexOf(nextC);
              if (cIdx < courseObj.courses.length - 1) {
                nextC = courseObj.courses[cIdx + 1];
                nextH = 0;
                if (state.activeViewCourse !== "ALL") {
                  state.activeViewCourse = nextC;
                }
              } else {
                nextH = 8;
              }
            }
            openScoreKeypad(0, nextC, nextH);
          });

          document.getElementById("clearSignatureBtn").addEventListener("click", () => {
            state.signatures[state.activeSignerKey] = null;
            persistState();
            renderSignArea();
            showToast("선택된 서명을 지웠습니다.");
          });

          document.getElementById("saveBtn").addEventListener("click", () => {
            const ok = persistState();
            if (ok) {
              playStepTap(true);
              showToast("구장, 점수, 서명 기록이 안전하게 저장되었습니다.");
            } else {
              showToast("브라우저 저장 공간을 사용할 수 없습니다.");
            }
          });

          document.getElementById("copyShareBtn").addEventListener("click", async () => {
            const shareText = buildShareText();
            const ok = await copyTextToClipboard(shareText);
            if (ok) {
              playStepTap(true);
              showToast("복사 완료! 카카오톡에 바로 붙여넣기 하세요.");
            } else {
              document.getElementById("shareFallbackText").value = shareText;
              document.getElementById("shareFallbackModal").classList.add("open");
            }
          });

          document.getElementById("resetBtn").addEventListener("click", () => {
            document.getElementById("resetModal").classList.add("open");
            document.getElementById("cancelResetBtn").focus();
          });

          document.getElementById("cancelResetBtn").addEventListener("click", () => {
            document.getElementById("resetModal").classList.remove("open");
          });

          document.getElementById("confirmResetScoresBtn").addEventListener("click", () => {
            state.players.forEach((pl) => {
              pl.scores = createEmptyScores();
            });
            state.signatures = { rep: null, p0: null, p1: null, p2: null, p3: null };
            const courseObj = getCourseObj(state.selectedCourseId);
            state.activeViewCourse = courseObj.courses[0];
            persistState();
            document.getElementById("resetModal").classList.remove("open");
            renderAll();
            showToast("모든 점수와 서명을 초기화했습니다.");
          });

          document.getElementById("confirmResetAllBtn").addEventListener("click", () => {
            const keepSound = state.soundEnabled;
            const keepCourse = state.selectedCourseId;
            state = createInitialState();
            state.soundEnabled = keepSound;
            state.selectedCourseId = keepCourse;
            persistState();
            document.getElementById("resetModal").classList.remove("open");
            renderAll();
            showToast("새 게임을 처음부터 시작합니다.");
          });

          document.getElementById("hioCloseBtn").addEventListener("click", () => {
            document.getElementById("holeInOneModal").classList.remove("open");
          });

          document.getElementById("hioReplayBtn").addEventListener("click", () => {
            playHoleInOneFanfare(true);
          });

          document.getElementById("shareFallbackCopyBtn").addEventListener("click", async () => {
            const text = document.getElementById("shareFallbackText").value;
            const ok = await copyTextToClipboard(text);
            if (ok) {
              document.getElementById("shareFallbackModal").classList.remove("open");
              showToast("복사 완료! 카카오톡에 바로 붙여넣기 하세요.");
            }
          });

          document.getElementById("shareFallbackCloseBtn").addEventListener("click", () => {
            document.getElementById("shareFallbackModal").classList.remove("open");
          });

          document.querySelectorAll(".modal-backdrop").forEach((backdrop) => {
            backdrop.addEventListener("click", (e) => {
              if (e.target === backdrop) {
                backdrop.classList.remove("open");
              }
            });
          });
        }

        renderTodayDate();
        bindEvents();
        renderAll();
      })();
    </script>
  </body>
</html>

{
  "name": "우리가족 파크골프 스코어카드",
  "description": "야외 햇빛 아래에서도 시니어분들이 눈이 편안하고 손가락으로 누르기 쉬운 파크골프 타수 기록 및 자동 합계 웹 앱",
  "requestFramePermissions": [],
  "majorCapabilities": []
}

{
  "name": "react-example",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite --port=3000 --host=0.0.0.0",
    "build": "vite build",
    "preview": "vite preview",
    "clean": "rm -rf dist server.js",
    "lint": "tsc --noEmit"
  },
  "dependencies": {
    "@google/genai": "^2.4.0",
    "@tailwindcss/vite": "^4.3.3",
    "@vitejs/plugin-react": "^6.1.1",
    "lucide-react": "^0.546.0",
    "react": "^19.0.1",
    "react-dom": "^19.0.1",
    "vite": "^8.3.0",
    "express": "^4.21.2",
    "dotenv": "^17.2.3",
    "motion": "^12.23.24"
  },
  "devDependencies": {
    "@types/node": "^22.14.0",
    "@types/react": "^19.3.0",
    "@types/react-dom": "^19.3.0",
    "autoprefixer": "^10.4.21",
    "esbuild": "^0.25.0",
    "tailwindcss": "^4.3.3",
    "tsx": "^4.21.0",
    "typescript": "^7.0.2",
    "@types/express": "^4.17.21"
  }
}

<div align="center">
<img width="1200" height="475" alt="GHBanner" src="https://ai.google.dev/static/site-assets/images/share-ais-513315318.png" />
</div>

# Run and deploy your AI Studio app

This contains everything you need to run your app locally.

View your app in AI Studio: https://ai.studio/apps/3f820327-b3db-4e46-b5d3-35f37822e3bc

## Run Locally

**Prerequisites:**  Node.js


1. Install dependencies:
   `npm install`
2. Set the `GEMINI_API_KEY` in [.env.local](.env.local) to your Gemini API key
3. Run the app:
   `npm run dev`

{
  "compilerOptions": {
    "target": "ES2022",
    "experimentalDecorators": true,
    "useDefineForClassFields": false,
    "module": "ESNext",
    "types": ["vite/client"],
    "lib": [
      "ES2022",
      "DOM",
      "DOM.Iterable"
    ],
    "skipLibCheck": true,
    "moduleResolution": "bundler",
    "isolatedModules": true,
    "moduleDetection": "force",
    "allowJs": true,
    "jsx": "react-jsx",
    "paths": {
      "@/*": [
        "./*"
      ]
    },
    "allowImportingTsExtensions": true,
    "noEmit": true
  },
  "exclude": ["dist"]
}

import tailwindcss from '@tailwindcss/vite';
import react from '@vitejs/plugin-react';
import fs from 'fs';
import path from 'path';
import {defineConfig} from 'vite';

export default defineConfig(() => {
  return {
    plugins: [
      react(),
      tailwindcss(),
      // Copies src/assets into dist/ so root-relative URLs like
      // "/src/assets/images/..." (e.g. generate_image output) still resolve
      // in production builds. Do not remove.
      {
        name: 'copy-unbundled-src-assets',
        apply: 'build',
        closeBundle(error?: Error): void {
          if (error) {
            return;
          }
          const distDir = path.resolve(__dirname, 'dist');
          const srcAssets = path.resolve(__dirname, 'src/assets');
          const distAssets = path.resolve(distDir, 'src/assets');
          if (fs.existsSync(distDir) && fs.existsSync(srcAssets)) {
            fs.cpSync(srcAssets, distAssets, {recursive: true, force: true});
          }
        },
      },
    ],
    resolve: {
      alias: {
        '@': path.resolve(__dirname, '.'),
      },
    },
    server: {
      // HMR is disabled in AI Studio via DISABLE_HMR env var.
      // Do not modify—file watching is disabled to prevent flickering during agent edits.
      hmr: process.env.DISABLE_HMR !== 'true',
      // Disable file watching when DISABLE_HMR is true to save CPU during agent edits.
      watch: process.env.DISABLE_HMR === 'true' ? null : {},
    },
  };
});

@import "tailwindcss";

import {createRoot} from 'react-dom/client';
import App from './App.tsx';
import './index.css';

createRoot(document.getElementById('root')!).render(<App />);

/**
 * @license
 * SPDX-License-Identifier: Apache-2.0
 */

export default function App() {
  return <div></div>;
}

# GEMINI_API_KEY: Required for Gemini AI API calls.
# AI Studio automatically injects this at runtime from user secrets.
# Users configure this via the Secrets panel in the AI Studio UI.
GEMINI_API_KEY="MY_GEMINI_API_KEY"

# APP_URL: The URL where this applet is hosted.
# AI Studio automatically injects this at runtime with the Cloud Run service URL.
# Used for self-referential links, OAuth callbacks, and API endpoints.
APP_URL="MY_APP_URL"
