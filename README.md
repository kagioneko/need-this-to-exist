# 💡 Need This To Exist (これ作って！)

「技術的には作れるはずなのに、なぜか世の中にちょうど良い製品が存在しない。」  
そんな世の中のニッチなペインポイント（不満・要望）と製品アイデアを、AI「ちぐら」と人間のブレインストーミングによって収集・放流するオープンソース・アイデアファクトリーです。

---

## ☕ Support / Patron (パトロン募集)
もしここに並んでいるアイデアの中で**「これは本当に欲しい！」「お金を払ってでも買いたい！」**というものがあれば、ぜひ以下のリンクからサポート（投票・寄付）をお願いします！  
支援が集まったアイデアは、私たちが実際に設計図（CAD）、基板データ、またはオープンソースコードを開発して公開します。

*   **Buy Me a Coffee**: `https://www.buymeacoffee.com/your_username` (準備中)
*   **GitHub Sponsors**: [kagioneko](https://github.com/sponsors/kagioneko)

---

## 🛠️ For Developers (開発者の方へ)
ここに掲載されているアイデアは、すべて **CC0（パブリックドメイン）** です。  
*   自由に実装して、ご自身のプロダクトとしてBOOTH、メルカリ、App Store、あるいはKickstarter等で**商用販売して大儲けしていただいて構いません**。ライセンス費用や報告の義務は一切ありません。
*   もし製品化したら、このリポジトリの該当アイデア部分に「実装例・販売リンク」として掲載しますので、プルリクエストや Issue でお気軽に教えてください！

---

## 🗂️ Ideas Showcase (アイデア一覧)

### 1. 🚨 物理式スマート『緊急ボスが来たボタン（Boss Button）』
*   **Category**: Hardware / Gadget
*   **Pain Point**: 席を外す時や、急に部屋に誰かが入ってきた際、画面ロックだけでは「直前まで何をしていたか」で気まずい思いをすることがある。ショートカットだと焦って押し間違える。
*   **Solution**: デスクの端に置ける、大きな赤い「非常停止スイッチ型」のUSB物理ボタン。押すとPC側で「指定したブラウザタブを一瞬で消し去り、ダミーのExcelスプレッドシートやソースコードを全画面表示」する。
*   **Why it doesn't exist**: 自作キーボードの文脈で作れるが、一般人がPCに挿すだけで使える「オシャレで可愛い専用ガジェット」は市販されていない。
*   **Status**: 💡 Idea (パトロン・開発者募集中)
*   **🛠️ DIY Recipe (自分で作るレシピ)**:
    *   **必要なハードウェア**:
        1.  `Raspberry Pi Pico` (または任意のRP2040マイコンボード) ➔ 約500〜800円
        2.  `非常停止スイッチ` (モメンタリ型 / 押している間だけONになるもの) ➔ 約300円
        3.  `ジャンパワイヤ` 2本、`MicroUSBケーブル`
    *   **配線図**:
        *   スイッチの端子A ➔ Picoの `GP15` (Pin 20)
        *   スイッチの端子B ➔ Picoの `GND` (任意のGroundピン)
    *   **ソフトウェア (CircuitPythonサンプルコード)**:
        PicoにCircuitPythonをインストールし、`code.py` として保存します。(`adafruit_hid` ライブラリが必要です)
        ```python
        import time
        import board
        import digitalio
        import usb_hid
        from adafruit_hid.keyboard import Keyboard
        from adafruit_hid.keycode import Keycode

        # GP15ピンをプルアップで初期化
        button = digitalio.DigitalInOut(board.GP15)
        button.direction = digitalio.Direction.INPUT
        button.pull = digitalio.Pull.UP

        kbd = Keyboard(usb_hid.devices)

        while True:
            if not button.value:  # ボタンが押された（GNDに接続された）時
                # Windows用: Alt + F4 (Macの場合は Keycode.COMMAND, Keycode.W などに変更)
                kbd.send(Keycode.ALT, Keycode.F4)
                time.sleep(1)  # チャタリング＆連打防止用のウェイト
            time.sleep(0.05)
        ```

---

### 2. 🎴 E-Ink製・卓上ステータス表示器『FocusPlate』
*   **Category**: Hardware / IoT
*   **Pain Point**: コワーキングスペースやリモートワーク中、周囲に「今は集中しているから話しかけないで」「今会議中」「今は雑談OK」という状態をいちいち説明するのが面倒。Slackステータスは画面を見ないと分からない。
*   **Solution**: デスクに置く、木製スタンド付きの小さな電子ペーパー（E-Ink）ディスプレイ。PCのSlack、Googleカレンダー、Zoomと自動同期し、現在のステータスをオシャレに物理表示する。
*   **Why it doesn't exist**: Alexaなどの液晶ディスプレイは派手で眩しくインテリアに馴染まないが、ミニマルで省電力な電子ペーパー製の専用表示器はない。
*   **Status**: 💡 Idea (パトロン・開発者募集中)

---

### 3. 🌧️ PCファンノイズを雨音にする『Fan Camouflage』
*   **Category**: Software (Windows / macOS)
*   **Pain Point**: AI画像生成やゲームでPCが高熱になるとファンが爆音で回り出し、その音が気になって集中できない。
*   **Solution**: GPU/CPU温度をリアルタイム監視し、ファンの物理的な風切り音の周波数に合わせて、スピーカーから心地よい「雨の音」や「焚き火の音（ホワイトノイズ）」を自動でミックスして流し、ファンの音を心理的にカモフラージュするアプリ。
*   **Why it doesn't exist**: ファン回転速度を下げるソフトはあるが、ファンの音を逆手に取って環境音で隠す心理的アプローチのアプリはない。
*   **Status**: 💡 Idea (パトロン・開発者募集中)

---

### 4. 🔑 2FAコード専用のスマートキーホルダー『AuthKey』
*   **Category**: Hardware / Security
*   **Pain Point**: ログイン時の二段階認証（2FA）コードを入力する際、いちいちスマホをロック解除してアプリを開くのが非常に面倒。
*   **Solution**: 車のスマートキーサイズの、超小型液晶キーホルダー。PCとUSB同期し、現在の6桁のコードが常に画面に表示されている。物理ボタンで複数のサービス（GitHub、Discord等）を切り替え可能。
*   **Why it doesn't exist**: 画面のないYubikeyや、スマホアプリはあるが、手元でパッと目視できるコンシューマー向けの「ミニ画面付き2FAキーホルダー」は存在しない。
*   **Status**: 💡 Idea (パトロン・開発者募集中)

---

### 5. ☘️ リアルGitHubの「草」育成ミニテラリウム『CommitMoss』
*   **Category**: Hardware / IoT
*   **Pain Point**: プログラマーはGitHubで毎日コミットして「草」を生やすことに執念を燃やしているが、画面上の緑のドットを見るだけでは、日々の努力が現実世界に還元されている感覚（物理的な達成感）が薄い。
*   **Solution**: デスク上に置く、自動給水機能付きのスマート苔（コケ）テラリウム。GitHub APIと連携し、コミットを検知すると「シュッ」と自動で水がスプレーされ、LEDの育成ライトが優しく光る。コミットを数日サボると給水がストップし、LEDも薄暗くなって苔が乾き始めるため、物理的に「草を生やし続けなければならない」強力なモチベーションが生まれる。
*   **Why it doesn't exist**: 画面上に草を模したウィジェットを表示するソフトウェアや、単なる時間管理型のスマートプランターは存在するが、プログラマーの「GitHubの草」というカルチャーと完全に同期し、デスクに飾れる美しいインテリアとして最適化されたIoTデバイスは存在しない。
*   **Status**: 💡 Idea (パトロン・開発者募集中)

---

### 6. 🕶️ オープンソースDIYスマートグラス『ChiguraGlass (OpenAR)』
*   **Category**: Hardware / IoT / Wearable
*   **Pain Point**: 映画『アイアンマン』のように視界にヘッドアップディスプレイ（HUD）でナビや翻訳テキストを浮かび上がらせたいが、Apple Vision Proは重くて高価すぎ、市販のARグラスも独自のクローズドなアプリが必要で、自由にハックできない。
*   **Solution**: 3Dプリンターで印刷したメガネフレームに、指先サイズのWi-Fiマイコン（ESP32-S3）と超小型OLED、そして45度に傾けたハーフミラーアクリル板を組み込んだ、総額数千円で自作できるオープンソースのARグラス。
*   **Why it doesn't exist**: 企業製のスマートグラスは「カメラによる盗撮懸念」や「高価格化」で一般に普及していないが、ハッカーが自分の欲しい機能（ナビ、通知、翻訳）だけをMicroPython等で自由にプログラムして動かせる「自作のための基本レシピ」が体系化されていない。
*   **Status**: 💡 Idea (パトロン・開発者募集中)
*   **🛠️ DIY Recipe (自分で作るレシピ)**:
    *   **必要なハードウェア**:
        1.  `ESP32-S3-Mini` (Wi-Fi/Bluetooth搭載マイコン) ➔ 約800円
        2.  `0.96インチ OLEDディスプレイ` (緑または青の単色発光がSF風で最適) ➔ 約500円
        3.  `ハーフミラーアクリル板 (1mm厚)` ➔ 約300円
        4.  `焦点距離の短いミニ凸レンズ (プラスチック)` (ピント調整用)
        5.  `超小型リチウムポリマーバッテリー (3.7V)`
    *   **光学配置 (Optics Diagram)**:
        *   `[OLEDディスプレイ]` ➔ `[凸レンズ]` ➔ (光が進む) ➔ `[斜め45度に置いたハーフミラー板]` ➔ (反射して目に入る ＋ 前方の景色も透けて見える)
    *   **ソフトウェア (ESP32 / MicroPythonサンプルコード)**:
        Bluetooth経由でスマホからテキストデータを受け取り、OLED画面に表示する基本の受信ループです。(`ssd1306` ライブラリが必要です)
        ```python
        import machine
        import ssd1306
        import time

        # I2C接続でOLEDの初期化 (GP8=SDA, GP9=SCL)
        i2c = machine.I2C(0, sda=machine.Pin(8), scl=machine.Pin(9))
        oled = ssd1306.SSD1306_I2C(128, 64, i2c)

        def display_hud_text(text):
            oled.fill(0) # 画面クリア
            # 視界の隅に綺麗に収まるように折り返して描画
            words = text.split(' ')
            line = 0
            for i in range(0, len(words), 2):
                msg = " ".join(words[i:i+2])
                oled.text(msg, 0, line * 12)
                line += 1
            oled.show()

        # ※実際はここでBluetooth SPPやBLEを起動して待機
        # スマホから「TURN RIGHT 100m」などの通知データを受信して display_hud_text() に渡します
        display_hud_text("CHIGURA OS v1.0")
        ```

---

## 🔄 Recycle & Reuse (古いデバイスの流用)

家庭で使わなくなった古いスマートフォン（Android/iPhone）や古いPCを、再び役立つスマートデバイスとして再生させるためのDIYレシピです。

---

### 7. 📱 古いスマホで作る『自作タッチ式マクロパッド (DeckPhone)』
*   **Category**: Software / Smartphone Reuse
*   **Pain Point**: アプリの起動やマイクのミュート、特定の操作をワンタップで実行できる「Stream Deck」は便利だが、高価で手が出しにくい。
*   **Solution**: 使わなくなった古いスマホ（Android / iOS）をPCの横にスタンドで置き、ブラウザで自作のWebボタン画面を表示。ボタンをタップすると、ローカルネットワーク経由（WebSocket）でPC側で登録したショートカットやアプリが一瞬でトリガーされる。
*   **Why it doesn't exist**: 同様の市販アプリ（有料）はあるが、広告があったり、PC側に重い専用クライアントが必要だったりする。完全にローカル完結で、HTMLとPythonの短いコードだけで自由にボタンデザインやショートカットを自作・拡張できるシンプルなOSSレシピが少ない。
*   **Status**: 💡 Idea (パトロン・開発者募集中)
*   **🛠️ DIY Recipe (自分で作るレシピ)**:
    *   **必要なハードウェア**:
        1.  `古いスマートフォン` (Wi-Fiが繋がればAndroid / iPhoneどちらでもOK)
        2.  `スマホスタンド`、`給電用ケーブル`
        3.  `ホストPC` (Windows / macOS / Linux)
    *   **ソフトウェア構成**:
        *   スマホのブラウザでPCのローカルIP（例: `http://192.168.1.XX:8080`）で立ち上げたWebサーバーにアクセスし、ボタン画面を表示。
        *   PC側では Python で WebSocket サーバーを常時起動し、スマホからの信号を受け取って `pyautogui` でキー入力をシミュレートする。
    *   **PC側 (Python WebSocket受信 & キー入力シミュレータ)**:
        `pip install websockets pyautogui` を実行して、以下の `deck_server.py` を実行します。
        ```python
        import asyncio
        import websockets
        import pyautogui
        import subprocess

        async def handler(websocket):
            print("[*] Smartphone connected!")
            async for message in websocket:
                print(f"[*] Received command: {message}")
                if message == "mute":
                    # Zoom/Discord等のミュートキー（例: Ctrl+Shift+M）をシミュレート
                    pyautogui.hotkey('ctrl', 'shift', 'm')
                elif message == "vscode":
                    # VSCodeを起動
                    subprocess.Popen(["code"])
                elif message == "calc":
                    # 電卓を起動
                    subprocess.Popen(["calc" if pyautogui.platform == "win32" else "open", "-a", "Calculator"])

        async def main():
            # ポート 8765 でWebSocketサーバーを起動
            async with websockets.serve(handler, "0.0.0.0", 8765):
                await asyncio.Future()  # 永続待機

        if __name__ == "__main__":
            asyncio.run(main())
        ```
    *   **スマホ側 (ブラウザ用簡易UI `index.html`)**:
        PCと同じWi-Fiに接続し、PCのIPアドレスを指定してブラウザで開きます。
        ```html
        <!DOCTYPE html>
        <html>
        <head>
            <meta charset="utf-8">
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <title>DeckPhone</title>
            <style>
                body { background: #121212; color: #fff; font-family: sans-serif; display: grid; grid-template-columns: repeat(2, 1fr); gap: 20px; padding: 20px; }
                button { background: #1e1e1e; color: #fff; border: 2px solid #333; border-radius: 15px; padding: 30px; font-size: 18px; font-weight: bold; }
                button:active { background: #333; }
            </style>
        </head>
        <body>
            <button onclick="sendCmd('mute')">🎙️ Mute</button>
            <button onclick="sendCmd('vscode')">💻 VS Code</button>
            <button onclick="sendCmd('calc')">🧮 Calculator</button>
            <script>
                // PCのローカルIPアドレスを指定して接続
                const ws = new WebSocket("ws://192.168.1.XX:8765");
                function sendCmd(cmd) {
                    if (ws.readyState === WebSocket.OPEN) {
                        ws.send(cmd);
                    }
                }
            </script>
        </body>
        </html>
        ```

---

### 8. ⌨️ メンブレンキーボード基板で作る『プログラム不要の物理USBスイッチ (Board Hijacker)』
*   **Category**: Hardware / Recycle & Reuse
*   **Pain Point**: 物理的なUSBボタンや自作フットペダルを作りたいが、マイコン（Raspberry Pi Picoなど）を買ってC言語やPythonでプログラムを書いてファームウェアを書き込むのが難しく、ハードルが高い。
*   **Solution**: 壊れた安いメンブレンキーボードやパンタグラフキーボードを分解し、中に入っている「USBケーブルが繋がった消しゴムサイズの制御基板」だけを抜き出す。特定の接点（ピン）同士を物理スイッチと配線して繋ぐだけで、プログラムを1行も書くことなく、PCが認識する物理USBスイッチを自作する。
*   **Why it doesn't exist**: 自作キーボードの入門として「キーボード基板の乗っ取り」は有名だが、プログラミングやマイコンが不要で安価な壊れた周辺機器だけで完結する、初心者に最も優しい物理スイッチDIYの「配線テスト手法とレシピ」がまとまったOSSドキュメントがない。
*   **Status**: 💡 Idea (パトロン・開発者募集中)
*   **🛠️ DIY Recipe (自分で作るレシピ)**:
    *   **必要なハードウェア**:
        1.  `壊れたメンブレンまたはパンタグラフキーボード` (安価なUSB接続のもの)
        2.  `物理スイッチ` (非常停止ボタン、または壊れたマウスから取り出したクリックボタン) ➔ 約300円
        3.  `導電ワイヤ`、`ハンダごて`
    *   **ハック手順 (Hijack Steps)**:
        1.  キーボードの裏ネジを全て外し、分解して緑色の「USB制御基板」を取り出す。
        2.  基板の下部にある、元々フィルム基板が接触していた金属ピン（通常16〜26本程度並んでいる）を確認する。
        3.  PCに基板をUSB接続し、メモ帳を開く。ピンセットや針金で、金属ピン同士を2箇所ずつ適当に通電（ショート）させてみる。
        4.  通電させた時にメモ帳に文字（例: `A` や `Space` や `Enter`）が入力されたら、その2つのピンの場所を記録する。
        5.  その2つのピンに対して、物理スイッチの2本の足をハンダ付けして配線する。
        6.  ボタンを押すと、PCにその文字が入力される「物理USBスイッチ」が完成！PC側でそのキー（例: `Space`）をミュートなどのショートカットに割り当てるだけで、プログラム不要で連動します。

## 🤖 Generated by Chigura
このリポジトリは、AI「ちぐら」が海外のペインポイント掲示板（Reddit等）から自動収集したアイデアと、人間とのブレインストーミングによって常に更新され続けます。
