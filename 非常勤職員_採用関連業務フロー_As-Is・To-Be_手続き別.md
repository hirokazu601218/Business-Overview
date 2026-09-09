# 非常勤職員 採用関連業務フロー（As-Is・To-Be／手続き別）

## 1. 本資料の位置付け

本資料は、非常勤職員の採用関連業務について、AからGまでの手続きごとにAs-IsとTo-Beの業務フローを対比するための構成確認資料である。

上司および現場ユーザーとの認識合わせを目的とし、最終的なPowerPoint業務フロー図を作成する前段階として使用する。To-Beは現時点の見直し案であり、業務確認および要件定義を通じて更新する。

### 表現ルール

- 青：通常の業務・アプリ内処理
- 橙：手作業、転記、紙またはExcel中心の処理
- 緑：システム連携、電子化または再利用
- 赤：現行業務の主な課題
- 灰：帳票、ファイル、開始・終了または補足
- A・B・Fは通常の非常勤職員のみを対象とし、調査員は対象外とする。

---

## 2. 手続きA｜内定手続き

### 2.1 As-Is

```mermaid
flowchart LR
    S([内定手続き開始]):::terminal

    subgraph L1[局担当者]
        direction LR
        A1[初任給決定調書を<br/>Excelで作成]:::manual
        A3[指摘内容を確認し<br/>Excelを修正]:::manual
    end

    subgraph L2[秘書課]
        direction LR
        A2[初任給決定調書の<br/>内容を確認]:::process
        D1{修正が必要か}:::decision
        A4[初任給の内容を確定]:::process
    end

    E([手続きBへ]):::terminal
    P1[課題：Excel作成と<br/>確認・修正が人手中心]:::issue

    S --> A1 --> A2 --> D1
    D1 -->|あり| A3 --> A2
    D1 -->|なし| A4 --> E
    A1 -.-> P1

    classDef process fill:#EAF3FA,stroke:#5B9BD5,color:#172033,stroke-width:1.5px;
    classDef manual fill:#FFF4E5,stroke:#D97706,color:#172033,stroke-width:1.5px;
    classDef decision fill:#FFF9DB,stroke:#B58900,color:#172033,stroke-width:1.5px;
    classDef issue fill:#FDECEC,stroke:#C00000,color:#8B0000,stroke-width:1.5px;
    classDef terminal fill:#F3F4F6,stroke:#7A8797,color:#172033,stroke-width:1.5px;
```

> 「秘書課との調整」を確認・修正の往復として可視化している。具体的な提出方法と確定権限は現場確認事項とする。

### 2.2 To-Be

```mermaid
flowchart LR
    S([内定手続き開始]):::terminal

    subgraph L1[局担当者]
        direction LR
        A1[簡易画面へ入力<br/>またはExcelを取込]:::app
        A4[表示された不備を修正]:::app
    end

    subgraph L2[異動情報アプリ]
        direction LR
        A2[必須項目・形式・<br/>データ内容を検証]:::app
        A3[初任給決定調書を出力]:::integration
    end

    subgraph L3[秘書課]
        direction LR
        A5[登録内容と帳票を確認]:::process
        D1{修正が必要か}:::decision
        A6[初任給の内容を確定]:::process
    end

    E([手続きBへ]):::terminal
    R1[見直し：最初からアプリに登録し<br/>帳票作成と入力検証に再利用]:::improve

    S --> A1 --> A2 --> A3 --> A5 --> D1
    D1 -->|あり| A4 --> A2
    D1 -->|なし| A6 --> E
    A2 -.-> R1

    classDef process fill:#EAF3FA,stroke:#5B9BD5,color:#172033,stroke-width:1.5px;
    classDef app fill:#E8F1FF,stroke:#2563EB,color:#172033,stroke-width:1.5px;
    classDef integration fill:#E8F5EE,stroke:#059669,color:#14532D,stroke-width:1.5px;
    classDef improve fill:#ECFDF5,stroke:#059669,color:#14532D,stroke-width:1.5px;
    classDef decision fill:#FFF9DB,stroke:#B58900,color:#172033,stroke-width:1.5px;
    classDef terminal fill:#F3F4F6,stroke:#7A8797,color:#172033,stroke-width:1.5px;
```

---

## 3. 手続きB｜採用起案

### 3.1 As-Is

```mermaid
flowchart LR
    S([手続きA完了]):::terminal

    subgraph L1[局担当者]
        direction LR
        B1[辞令案をWordで作成]:::manual
        B2[年間予算使用見込等を<br/>Excelで作成]:::manual
        B3[初任給決定調書と<br/>関係書類を取りまとめ]:::manual
        B4[EASYで採用起案を申請]:::process
    end

    subgraph L2[EASY・決裁者]
        direction LR
        B5[起案内容を確認・決裁]:::process
    end

    E([手続きCへ]):::terminal
    P1[課題：複数のWord・Excelを<br/>個別作成して添付]:::issue

    S --> B1 --> B2 --> B3 --> B4 --> B5 --> E
    B1 -.-> P1
    B2 -.-> P1

    classDef process fill:#EAF3FA,stroke:#5B9BD5,color:#172033,stroke-width:1.5px;
    classDef manual fill:#FFF4E5,stroke:#D97706,color:#172033,stroke-width:1.5px;
    classDef issue fill:#FDECEC,stroke:#C00000,color:#8B0000,stroke-width:1.5px;
    classDef terminal fill:#F3F4F6,stroke:#7A8797,color:#172033,stroke-width:1.5px;
```

### 3.2 To-Be

```mermaid
flowchart LR
    S([手続きA完了]):::terminal

    subgraph L1[局担当者]
        direction LR
        B1[登録済み情報を確認]:::process
        B3[出力帳票を確認し<br/>EASYで採用起案を申請]:::process
    end

    subgraph L2[異動情報アプリ]
        direction LR
        B2[初任給決定調書・辞令案・<br/>起案用データを出力]:::integration
    end

    subgraph L3[EASY・決裁者]
        direction LR
        B4[起案内容を確認・決裁]:::process
    end

    E([手続きCへ]):::terminal
    R1[見直し：登録済みデータを再利用し<br/>帳票の重複入力を削減]:::improve

    S --> B1 --> B2 --> B3 --> B4 --> E
    B2 -.-> R1

    classDef process fill:#EAF3FA,stroke:#5B9BD5,color:#172033,stroke-width:1.5px;
    classDef integration fill:#E8F5EE,stroke:#059669,color:#14532D,stroke-width:1.5px;
    classDef improve fill:#ECFDF5,stroke:#059669,color:#14532D,stroke-width:1.5px;
    classDef terminal fill:#F3F4F6,stroke:#7A8797,color:#172033,stroke-width:1.5px;
```

> EASYとの直接連携は現時点では前提とせず、アプリから出力した情報を起案に利用する構成としている。

---

## 4. 手続きC｜発令

### 4.1 As-Is

```mermaid
flowchart LR
    S([採用起案の決裁完了]):::terminal

    subgraph L1[局担当者]
        direction LR
        C1[起案情報を異動情報アプリへ<br/>手作業で転記]:::manual
    end

    subgraph L2[異動情報アプリ]
        direction LR
        C2[登録情報を保持]:::system
        C3[所定様式で辞令を出力]:::system
    end

    subgraph L3[秘書課]
        direction LR
        C4[登録内容を確認]:::process
        C5[辞令作成を指示]:::process
        C6[辞令を確認して発令]:::process
    end

    E([手続きD・E・F・Gへ]):::terminal
    P1[課題：起案済み情報を<br/>アプリへ再入力]:::issue

    S --> C1 --> C2 --> C4 --> C5 --> C3 --> C6 --> E
    C1 -.-> P1

    classDef process fill:#EAF3FA,stroke:#5B9BD5,color:#172033,stroke-width:1.5px;
    classDef manual fill:#FFF4E5,stroke:#D97706,color:#172033,stroke-width:1.5px;
    classDef system fill:#E8F1FF,stroke:#2563EB,color:#172033,stroke-width:1.5px;
    classDef issue fill:#FDECEC,stroke:#C00000,color:#8B0000,stroke-width:1.5px;
    classDef terminal fill:#F3F4F6,stroke:#7A8797,color:#172033,stroke-width:1.5px;
```

### 4.2 To-Be

```mermaid
flowchart LR
    S([通常職員：手続きB完了<br/>調査員：手続きCから開始]):::terminal

    subgraph L1[局担当者]
        direction LR
        C1[調査員の場合のみ<br/>発令情報を簡易入力]:::app
    end

    subgraph L2[異動情報アプリ]
        direction LR
        C2[通常職員はA・Bの<br/>登録情報をそのまま利用]:::integration
        C5[登録情報から辞令を出力]:::integration
    end

    subgraph L3[秘書課]
        direction LR
        C3[発令情報を確認]:::process
        C4[辞令作成を指示]:::process
        C6[辞令を確認して発令]:::process
    end

    E([手続きD・E・F・Gへ]):::terminal
    R1[見直し：前工程のデータを再利用し<br/>発令時の転記を廃止]:::improve

    S --> C2
    S -.->|調査員| C1 --> C3
    C2 --> C3 --> C4 --> C5 --> C6 --> E
    C2 -.-> R1

    classDef process fill:#EAF3FA,stroke:#5B9BD5,color:#172033,stroke-width:1.5px;
    classDef app fill:#E8F1FF,stroke:#2563EB,color:#172033,stroke-width:1.5px;
    classDef integration fill:#E8F5EE,stroke:#059669,color:#14532D,stroke-width:1.5px;
    classDef improve fill:#ECFDF5,stroke:#059669,color:#14532D,stroke-width:1.5px;
    classDef terminal fill:#F3F4F6,stroke:#7A8797,color:#172033,stroke-width:1.5px;
```

---

## 5. 手続きD｜職員DB登録・異動情報アプリ更新

### 5.1 As-Is

```mermaid
flowchart LR
    S([発令完了]):::terminal

    subgraph L1[秘書課]
        direction LR
        D1[採用者情報を職員DBへ登録]:::manual
        D4[Salesforceレポートから<br/>発行情報を出力]:::manual
        D5[発行情報を異動情報アプリへ<br/>手作業で反映]:::manual
    end

    subgraph L2[職員DB・Salesforce]
        direction LR
        D2[採用者情報を登録]:::system
        D3[職員番号・メールアドレスを発行]:::system
    end

    subgraph L3[異動情報アプリ]
        direction LR
        D6[発行情報を保持]:::system
    end

    E([登録完了]):::terminal
    P1[課題：職員DBから出力後<br/>アプリへ再入力]:::issue
    N1[要確認：職員DBへの<br/>具体的な登録方法]:::note

    S --> D1 --> D2 --> D3 --> D4 --> D5 --> D6 --> E
    D5 -.-> P1
    D1 -.-> N1

    classDef manual fill:#FFF4E5,stroke:#D97706,color:#172033,stroke-width:1.5px;
    classDef system fill:#E8F1FF,stroke:#2563EB,color:#172033,stroke-width:1.5px;
    classDef issue fill:#FDECEC,stroke:#C00000,color:#8B0000,stroke-width:1.5px;
    classDef note fill:#FFF9DB,stroke:#B58900,color:#6B4F00,stroke-width:1.5px;
    classDef terminal fill:#F3F4F6,stroke:#7A8797,color:#172033,stroke-width:1.5px;
```

### 5.2 To-Be

```mermaid
flowchart LR
    S([発令完了]):::terminal

    subgraph L1[異動情報アプリ]
        direction LR
        D1[採用者情報を連携]:::integration
        D5[職員番号・メールアドレスを<br/>登録情報へ反映]:::integration
        D6[秘書課・局担当者へ<br/>反映結果を表示]:::app
    end

    subgraph L2[職員DB]
        direction LR
        D2[採用者情報を登録]:::system
        D3[職員番号・メールアドレスを発行]:::system
        D4[発行情報を連携]:::integration
    end

    E([連携完了]):::terminal
    R1[見直し：職員DBとの連携により<br/>出力・再入力を廃止]:::improve

    S --> D1 --> D2 --> D3 --> D4 --> D5 --> D6 --> E
    D4 -.-> R1

    classDef app fill:#E8F1FF,stroke:#2563EB,color:#172033,stroke-width:1.5px;
    classDef system fill:#EAF3FA,stroke:#5B9BD5,color:#172033,stroke-width:1.5px;
    classDef integration fill:#E8F5EE,stroke:#059669,color:#14532D,stroke-width:1.5px;
    classDef improve fill:#ECFDF5,stroke:#059669,color:#14532D,stroke-width:1.5px;
    classDef terminal fill:#F3F4F6,stroke:#7A8797,color:#172033,stroke-width:1.5px;
```

---

## 6. 手続きE｜給与基本マスタへの登録

### 6.1 As-Is

```mermaid
flowchart LR
    S([異動情報アプリへの登録完了]):::terminal

    subgraph L1[会計課給与班]
        direction LR
        E1[異動情報アプリから<br/>Excelをダウンロード]:::manual
        E2[給与業務に必要な<br/>項目を確認]:::manual
        D1{情報が不足しているか}:::decision
        E3[Teamsチャットで<br/>局担当者へ確認]:::manual
        E5[回答内容を補完]:::manual
        E6[給与基本マスタへ<br/>手作業で登録]:::manual
    end

    subgraph L2[局担当者]
        direction LR
        E4[不足情報を回答]:::process
    end

    E([登録完了]):::terminal
    P1[課題：必須項目の不足確認と<br/>Excelへの手入力が発生]:::issue

    S --> E1 --> E2 --> D1
    D1 -->|あり| E3 --> E4 --> E5 --> E6
    D1 -->|なし| E6 --> E
    D1 -.-> P1

    classDef process fill:#EAF3FA,stroke:#5B9BD5,color:#172033,stroke-width:1.5px;
    classDef manual fill:#FFF4E5,stroke:#D97706,color:#172033,stroke-width:1.5px;
    classDef decision fill:#FFF9DB,stroke:#B58900,color:#172033,stroke-width:1.5px;
    classDef issue fill:#FDECEC,stroke:#C00000,color:#8B0000,stroke-width:1.5px;
    classDef terminal fill:#F3F4F6,stroke:#7A8797,color:#172033,stroke-width:1.5px;
```

### 6.2 To-Be

```mermaid
flowchart LR
    S([発令情報の登録完了]):::terminal

    subgraph L1[給与基本マスタアプリ]
        direction LR
        E1[異動情報アプリから<br/>給与計算に必要な情報を取得]:::integration
        E2[マスタ登録候補を作成]:::app
        E3[不足・不整合項目を検証]:::app
        D1{修正が必要か}:::decision
    end

    subgraph L2[局担当者・会計課給与班]
        direction LR
        E4[表示された項目を修正]:::app
        E5[会計課給与班が<br/>登録内容を確認・確定]:::process
    end

    E([登録完了]):::terminal
    R1[見直し：アプリ間でデータを取得し<br/>不足確認と転記を削減]:::improve

    S --> E1 --> E2 --> E3 --> D1
    D1 -->|あり| E4 --> E3
    D1 -->|なし| E5 --> E
    E1 -.-> R1

    classDef process fill:#EAF3FA,stroke:#5B9BD5,color:#172033,stroke-width:1.5px;
    classDef app fill:#E8F1FF,stroke:#2563EB,color:#172033,stroke-width:1.5px;
    classDef integration fill:#E8F5EE,stroke:#059669,color:#14532D,stroke-width:1.5px;
    classDef improve fill:#ECFDF5,stroke:#059669,color:#14532D,stroke-width:1.5px;
    classDef decision fill:#FFF9DB,stroke:#B58900,color:#172033,stroke-width:1.5px;
    classDef terminal fill:#F3F4F6,stroke:#7A8797,color:#172033,stroke-width:1.5px;
```

---

## 7. 手続きF｜通勤手当の認定

### 7.1 As-Is

```mermaid
flowchart LR
    S([発令完了]):::terminal

    subgraph L1[局担当者]
        direction LR
        F1[通勤届をExcelで作成]:::manual
        F2[共有フォルダへ格納]:::manual
        F3[Teamsチャネルで<br/>格納先を連絡]:::manual
    end

    subgraph L2[会計課給与班]
        direction LR
        F4[通勤届を取得して審査]:::manual
        F5[通勤手当を認定]:::process
        F6[別のExcelで<br/>認定簿を作成]:::manual
        F7[認定簿をPDF化して<br/>共有フォルダへ格納]:::manual
        F8[Teamsチャネルで<br/>完了を連絡]:::manual
    end

    E([認定完了]):::terminal
    P1[課題：申請・認定・認定簿が<br/>複数ファイルに分散]:::issue

    S --> F1 --> F2 --> F3 --> F4 --> F5 --> F6 --> F7 --> F8 --> E
    F6 -.-> P1

    classDef process fill:#EAF3FA,stroke:#5B9BD5,color:#172033,stroke-width:1.5px;
    classDef manual fill:#FFF4E5,stroke:#D97706,color:#172033,stroke-width:1.5px;
    classDef issue fill:#FDECEC,stroke:#C00000,color:#8B0000,stroke-width:1.5px;
    classDef terminal fill:#F3F4F6,stroke:#7A8797,color:#172033,stroke-width:1.5px;
```

### 7.2 To-Be

```mermaid
flowchart LR
    S([発令完了]):::terminal

    subgraph L1[局担当者]
        direction LR
        F1[給与基本マスタアプリへ<br/>通勤届情報を直接入力]:::app
        F5[不備内容を修正して再提出]:::app
    end

    subgraph L2[給与基本マスタアプリ]
        direction LR
        F2[必須項目・入力内容を検証]:::app
        F3[申請内容を会計課給与班へ表示]:::app
        F4[不備内容をアプリ上で通知]:::integration
        F7[認定情報から<br/>認定簿PDFを出力]:::integration
    end

    subgraph L3[会計課給与班]
        direction LR
        D1{不備があるか}:::decision
        F6[通勤手当を認定]:::process
    end

    E([認定完了]):::terminal
    R1[見直し：申請から認定簿出力までを<br/>同一アプリで一元管理]:::improve

    S --> F1 --> F2 --> F3 --> D1
    D1 -->|あり| F4 --> F5 --> F2
    D1 -->|なし| F6 --> F7 --> E
    F7 -.-> R1

    classDef process fill:#EAF3FA,stroke:#5B9BD5,color:#172033,stroke-width:1.5px;
    classDef app fill:#E8F1FF,stroke:#2563EB,color:#172033,stroke-width:1.5px;
    classDef integration fill:#E8F5EE,stroke:#059669,color:#14532D,stroke-width:1.5px;
    classDef improve fill:#ECFDF5,stroke:#059669,color:#14532D,stroke-width:1.5px;
    classDef decision fill:#FFF9DB,stroke:#B58900,color:#172033,stroke-width:1.5px;
    classDef terminal fill:#F3F4F6,stroke:#7A8797,color:#172033,stroke-width:1.5px;
```

> 手続きFは通常の非常勤職員のみを対象とし、調査員は対象外とする。

---

## 8. 手続きG｜外部機関との手続き

### 8.1 As-Is

```mermaid
flowchart LR
    S([発令完了]):::terminal

    subgraph L1[局担当者]
        direction LR
        G1[加入関係書類を<br/>手書きまたはExcelで作成]:::manual
        G2[社会保険・共済組合・<br/>ハローワークへ紙で提出]:::manual
        G4[決定通知書を受領]:::manual
        G5[共有フォルダへ格納]:::manual
        G6[Teamsチャットで<br/>会計課給与班へ連絡]:::manual
    end

    subgraph L2[外部機関]
        direction LR
        G3[届出を受理し<br/>決定通知書を発行]:::external
    end

    subgraph L3[会計課給与班]
        direction LR
        G7[通知内容を目視確認]:::manual
        G8[給与基本マスタへ手入力]:::manual
    end

    E([関連登録完了]):::terminal
    P1[課題：紙申請と通知書の受渡し、<br/>給与マスタへの手入力が発生]:::issue

    S --> G1 --> G2 --> G3 --> G4 --> G5 --> G6 --> G7 --> G8 --> E
    G2 -.-> P1
    G8 -.-> P1

    classDef manual fill:#FFF4E5,stroke:#D97706,color:#172033,stroke-width:1.5px;
    classDef external fill:#F3F4F6,stroke:#7A8797,color:#172033,stroke-width:1.5px;
    classDef issue fill:#FDECEC,stroke:#C00000,color:#8B0000,stroke-width:1.5px;
    classDef terminal fill:#F3F4F6,stroke:#7A8797,color:#172033,stroke-width:1.5px;
```

#### 転職者の住民税手続き（As-Is補足）

```mermaid
flowchart LR
    T1[局担当者が転職元へ連絡]:::manual
    T2[住民税異動届を受領]:::manual
    T3[共有フォルダへ格納し<br/>Teamsで連絡]:::manual
    T4[会計課給与班が目視確認]:::manual
    T5[給与基本マスタへ手入力]:::manual

    T1 --> T2 --> T3 --> T4 --> T5

    classDef manual fill:#FFF4E5,stroke:#D97706,color:#172033,stroke-width:1.5px;
```

### 8.2 To-Be

```mermaid
flowchart LR
    S([発令完了]):::terminal

    subgraph L1[局担当者]
        direction LR
        G1[給与基本マスタアプリへ<br/>加入手続情報を直接入力]:::app
        G3[アプリから電子申請を実行]:::app
    end

    subgraph L2[給与基本マスタアプリ]
        direction LR
        G2[必須項目・入力内容を検証]:::app
        G4[外部機関へ電子申請]:::integration
        G7[受付結果・決定情報を保持]:::integration
        G8[手続結果を担当者へ表示]:::app
    end

    subgraph L3[外部機関]
        direction LR
        G5[申請を受け付け]:::external
        G6[受付結果・決定通知を<br/>電子返却]:::integration
    end

    E([関連登録完了]):::terminal
    R1[見直し：紙と共有フォルダを介さず<br/>申請・結果を電子的に一元管理]:::improve

    S --> G1 --> G2 --> G3 --> G4 --> G5 --> G6 --> G7 --> G8 --> E
    G4 -.-> R1

    classDef app fill:#E8F1FF,stroke:#2563EB,color:#172033,stroke-width:1.5px;
    classDef integration fill:#E8F5EE,stroke:#059669,color:#14532D,stroke-width:1.5px;
    classDef improve fill:#ECFDF5,stroke:#059669,color:#14532D,stroke-width:1.5px;
    classDef external fill:#F3F4F6,stroke:#7A8797,color:#172033,stroke-width:1.5px;
    classDef terminal fill:#F3F4F6,stroke:#7A8797,color:#172033,stroke-width:1.5px;
```

#### 転職者の住民税手続き（To-Be補足）

```mermaid
flowchart LR
    T1[局担当者が住民税引継情報を<br/>給与基本マスタアプリへ入力]:::app
    T2[転職元または関係先へ<br/>電子連携]:::integration
    T3[住民税異動情報を<br/>電子返却]:::integration
    T4[住民税情報を<br/>アプリ上で表示・管理]:::app

    T1 --> T2 --> T3 --> T4

    classDef app fill:#E8F1FF,stroke:#2563EB,color:#172033,stroke-width:1.5px;
    classDef integration fill:#E8F5EE,stroke:#059669,color:#14532D,stroke-width:1.5px;
```

---

## 9. PowerPoint化に向けた確認事項

本資料を基に、手続きごとに次の事項を確認する。

1. As-Isの実施者、処理順序および受渡方法が実態と一致しているか。
2. 図中で補完した確認・修正の往復が実態と一致しているか。
3. 課題の位置と表現が適切か。
4. To-Beの役割分担およびアプリの範囲が適切か。
5. 外部機関との電子連携が制度・技術上可能か。
6. 各図を最終的に1手続き1枚とするか、複数手続きを1枚に統合するか。

## 10. 現時点の未確認事項

- 手続きAにおける初任給決定調書の提出方法、修正依頼方法および最終確定者
- 手続きBで実際に添付する書類の全件
- 職員DBへの具体的な登録方法
- 調査員について、C・D・E・Gに固有の差異があるか
- 通勤手当の認定結果を給与基本マスタへ反映する後続処理
- 外部機関ごとの電子申請・電子返却の実現方式

## 11. 更新履歴

| 版 | 更新日 | 更新内容 |
|---|---|---|
| 0.1 | 2026-09-10 | A～Gの手続き別As-Is・To-Beフロー初版を作成 |
