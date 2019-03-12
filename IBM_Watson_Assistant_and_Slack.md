Title: [【Watson×Slack】IBM Watsonを連携させたSlack botを開発する方法 (Watson Assistant編)](https://qiita.com/ayatokura/items/476139e76c73e6c88362)  
Author: @ayatokura  
Modification Date: 2019/3/12  
- - -

今回は、Watson APIを使ったSlack Botアプリの開発する手順をご紹介いたします。コーディングなしで進めることができますので、プログラミングに慣れていない方も触ってみてください。この操作を終えると、SlackにWatsonが連携されたSlack Botと自然な会話の流れでチャットを体験することができます。
※今回は、IBM WatsonとSlackの連携が簡単に行えることを解説するため、英語サンプルを利用していますが、実際はWatson Assistant上でカスタマイズすることで日本語も利用することが可能です。
【Slack bot完成後の例】
<img src="https://gf6mxw.by.files.1drv.com/y4mjIzZCDrGnqMTNkYdQiD22v27TyQWVdv1V-hwoiVhaYUku-VCy73YhJjHBcugGO9WxX-xEmM2OkJMTTNYC8pPwpa6WCNdVG78MbV2i9QZlYjAVhfpuCE41T1hgmkkDyksL96n2R_7CmHIfZra9TPpBYD0Ahdj22ehB8s4HUFAkwcWD_3Ce7GQa9lWKw8o_N1pMbw3mFs8T9KFeZ2GbEW0Mg?width=1660&height=714&cropmode=none" width="600">

## IBM Waton Assistantについて
**Watson Assistant**は、チャットボット等、ユーザーとコンピューターが自然言語で対話可能なアプリケーションを簡単に開発するためのAPIサービスです。
詳しくは、[Watson Assitant](https://www.ibm.com/watson/jp-ja/developercloud/conversation.html)サイトをご覧ください。

# 用意する環境と操作の流れ
## 必要なシステム
Webブラウザ上ですべての操作を行うため
* Webブラウザ (私のほうではChrome, Firefox環境で検証しました)
* インターネット接続
をご用意ください。

## 操作の流れ
今回は次の5つのステップで手順を解説しています。
所用時間目安は30分〜くらいです。Slack bot開発に慣れている方だともう少し早く完成させることが出来ると思います。
<img src="https://fq6lxw.by.files.1drv.com/y4m4YUl7EgyJ_t_U0HrBa0CIE5CyX_9n4ym-4JQ8Xzp0xWIS-jXUdyHf6P7dyvmss0rkOwgUxKGFA3B5X1CBjwQBq5N3strcwSUSRwGeQET_ISTXgeaKI_g1CX5q93Ck1BdJC_wtIgp_WedEV0NvXwf3bBEy4x_gVrSOWdanyYWKT9Th3VS0oN_WCdAdleZcRizbFQbSulW4lDgA9nnccp-Pw?width=772&height=113&cropmode=none" width="700">

# 1. IBM Cloud アカウント作成
IBM Watson Assistantサービスを利用するためには、**IBM Cloudアカウント**が必要です。
初めてIBM Cloudを利用される方は、[コチラ](https://ibm.biz/Bd2PtK)から無料で利用できるライトアカウント登録をしてください。
※メールアドレスのみの登録で始められます。

# 2. IBM Watson Assitantの作成
1. Webブラウザから[IBM Cloudダッシュボード](https://cloud.ibm.com/)へアクセスする。 
2. 「カタログ」→「AI」→「Watson Assistant」の順に選択する。   
<img src="https://gp6oxw.by.files.1drv.com/y4mblIReVzQnMr0Sz0FvCo0EQb3vRayVpqo94j0ZwhAb0BCPArjlCFh0r8Kv_sSlmDpYYA8R9muplNdZVqI1iS_1nyyjns84bpwEqckaWPGEus_gov3p6G-xGENIKFaWFXu_7aPiE8ShtLLHtuooNpYje4Fph_O3KLq9yErpM_WT4EPOTM3DNUYgiiuT1_zE7ZCCXKeB30zu3dY1UAjJ_vmIg?width=1610&height=1028&cropmode=none" width="600">
3. 「サービス名」に任意のサービス名を入力し、「作成」ボタンをクリックする。
<img src="https://gp6pxw.by.files.1drv.com/y4mP2gTEUpK90cn3gYUBB2JBJBShgLfJogSSWe7cxz559rnF_thqSN1heLT5QILP4iXnDQ_AwnHIdXa_78anIJ5AgGkOa9RmpQsF3WhVq7PBUMLIyXqMpgriD4tMxgYYj_dgPlV3eVB9LC2hGoAsHFizXng2xHSRJ_xI8B2P8b8cy96dLjt1Y1Z9BYtXJoT_Yc3tPuIfuudRIeFQxj5eSBwNw?width=1438&height=1152&cropmode=none" width="600">

# 3. IBM Watson Assitantの設定
<img src="" width="600">
1. 「ツールの起動」ボタンをクリックする。
<img src="https://gp6nxw.by.files.1drv.com/y4mhSqUQI04-FLd99g_4jeIhBI6kgHtpOqR7IzVRHP-jJelqtneeRHQnJc7L1A1IxqSh9U6nqxDil2CfnFxDl5An6bdbbjcsGKy2phj-brIl8hBH_xw-jwPsdx7FBSIWNQ-mGmtL5pOkPRACifBYWsCFpxzFKy_J1Ztc8lbyQ4j4w4TqtvxBBLkCbDnGw_csZSxNrB0acvKw5X0ODFtoYNN7w?width=1492&height=784&cropmode=none" width="600">
2. 「IBM Watson Assistant」画面が表示されたら「Skills」タブを開き、「Create new」をクリックする。
<img src="https://gp6mxw.by.files.1drv.com/y4mjdQAOOyTJcnpDr-HLMLcGbpUgUFXmcdzvsZn2DoFaXENWHhYZ6OXoHIif30QNQpT88Gf4vgVWktENFXLGP2JCuWJRKqTkNE7XWLv2Mp8E93gvDTnJWWfwKl9YUrxYTeRweYcZI36_t81rH5Mbx2OD98ue4Abg3aLK4KL5q2zgrEUIDrgVmZMn3mAdkWNaMbEeNFmLAZWoOzcVdo3Q2xWYw?width=1580&height=902&cropmode=none" width="600">
3. 「Add Dialog Skill」画面で今回は既存のサンプル(英語)を利用するため、「Use sample skill」タブより、「Customer Care Sample Skill」をクリックする。
<img src="https://gp6lxw.by.files.1drv.com/y4mDSgtOYAznaobdL_t90zf-yVF4LOEcA3x-Ws7TlPINi9HR0UGHHssifCJypEGJwXQJh3SuyWGhGxusUT4N3EFMO7kmBoXDT3u30WEEddixpSv1qOmaG8tENr_JBDEUKFEtrWFrbqXEUkWLEB9CzCdSRoaxoje1LiMTYUHBh49SQTB2jFNkIXzxQULIb7iFDy8P2eqXj0gEqjYXKm5Sq6tHg?width=1658&height=970&cropmode=none" width="600">
4. 「IBM Watson Assistant」をクリックし、「Assitant」タブより「Create new」ボタンをクリックする。
<img src="https://gp6kxw.by.files.1drv.com/y4mNmQf1HZp8UOGa-DSm9gt_nRkDGcx8iKrFfacfHk5K058zReUs7ldwpbLEcTfkaRgNCBGLUH3ldWISEcBMym3KJRoTrHkAKXHWVxIIFoMnmP3owTY8QsdVnr67zFy8DAEAvZPZLlFrgmTxD8ZClgYHFUuQ4kc7vZmB93o0HiVfdJUwyvd_eG5Q3MeEszBDh_7cCe24-90lqBBDo3UVLF2gQ?width=1746&height=1076&cropmode=none" width="600">
5. 「Name」に任意の名前を入力し、「Enable Preview Link」チェックを外した後、「Create」ボタンで次に進む。(例えば、今回の画面では「Customer Service Assistant」と入力しました。)
<img src="https://gp6jxw.by.files.1drv.com/y4mC4CDA0ujhFtutKtRFZNBqX8snTnxCQ2fiG27dEoHgXjqS6JxwXZ0KXkhPBR3Hdmgkwkza8WB7rM-Kb75hXrEzJ4-QtzNt7N4g1J37pWtWvI8jviJyrAuY2qslLuubNQwY2mwESrbF3_d-M86xHw-PkcOxF5kGOsDFbySpujn6PO93GFqIpyF8VubYcRfWjJOynJncD-a-OZftB5UDoM8Dw?width=1506&height=962&cropmode=none" width="600">
6. 作成した名前の画面が表示されたら、「Add Dialog Skill」ボタンをクリックする。
<img src="https://gp6ixw.by.files.1drv.com/y4mVVp-cp35A-XKY2hj1tNRW9QGX8CKOuRLq-XnNlFpskWnyxVH_Bl_vqNX22fZpTFD1JA3oPg7yWwHqzWXQckTrKCyLiq5uEu2pT8zqe4gjKOaqFPpDSGYLBXtq_mkC0iwHup_sjBK13FXm2DqFz52UUhqD-JU_aVVCuxHFb3TtOOVlChGjxdZzK34AqXFJ_nZ_2O5vQ2BTJBeUKOqjfSVIw?width=1680&height=1052&cropmode=none" width="600">
7. 「Add existing skill」タブが表示されている状態になっていることを確認し、ご自身で作成したSkillをクリックする。
<img src="https://gp6hxw.by.files.1drv.com/y4mPED7Fccxmkc4R95kEGfAOq99ZJ3H3SYp9tczCewkqVgST_T_N3AFGZ4kPNx_9Xv5eG4K_n4eGsSHtqaxLTZ1Cu9EwcABdl3uS9lvUh-kKlsVb5A8vnPIH8Rx7ZL9LcmzcOaxka-qVDrNYs0NIkH6-K9TizcN5ZgIhjVq9O3V8jILvkN9bkOq5zJWV4eRrzK0BRgVayD_XlO5ilXCrv8vlA?width=1846&height=1098&cropmode=none" width="600">
8. 「Add Integration」ボタンをクリックする。
<img src="https://gp6gxw.by.files.1drv.com/y4mGULXyRPB0k8iJfNTisodEPKht5Bz61fhLgheoIAcqe1urteUC5bG7pfwE1F7cDVGXGnbyVwNTv0V1Ti7D9gRPTKXqG4hVpabiIAnRDTBSoOHMLF_l7dqSAtzMcLFH3zeclqrVY_mAwmfiJFW4xPWkT-OBKfv6tT7O6FJfgdn6iHZ7pPTQKPuPlmPga3EJW5HyDKdqkHz1W4nbJb781ilhA?width=1660&height=1304&cropmode=none" width="600">
9. 「Add Integration」画面で「Slack」を選択する。
<img src="https://gf6oxw.by.files.1drv.com/y4m1cy-MI_6c76v9B71nIyTPNx63GZL7uE1p2RVifk9nJPhPuIaTy3K5Eu54JGWuxCzTlDfn5xtFqj3R-Y_K9WQrNul81-JqVT-1f2DO0CUkE8P5hPmHWhJpFvviItya4_1J9qcnTmWUp3QLzIf4pfi0Y5ArkjxdHZCPzXxbKezW0Dbpit0I9PCs1vfujFWPtqhmvk8KLHS9VeqlcHTU-I3yQ?width=1468&height=1202&cropmode=none" width="600">
10. 「Slack Integration」画面が表示されたら「Name」に任意の名前を入力する。(例えば、今回の画面では「Customer Service Integration」と入力しました。)
<img src="https://gf6pxw.by.files.1drv.com/y4mzf4TeejagE0MxFJBKchyQI-33tMu23o_FKX-1NTpovgWooHHz1c8djUyLBEiiKbKnPeuzuXxR6cCnK-00ELkLh43FHubli4YZlM2S70TindB_n5lXna7GHM_gVVx9KkRKlaG8xIbgzsjpui30TXNbrxB9zL5j3vVB0crD1QJryOjVx6R99SAv8wqqSWiN86UwnM5-HrGVjXudBA9zyZbXw?width=1864&height=738&cropmode=none" width="600">

#4. Slackとの連携を設定する
ここからはSlackサービスとの連携をするための操作になります。
事前にSlack Workspaceを用意しておいてください。
## 4-1 Slackの設定 (Configuration for Slack)
1. 「Create a Slack app」リンクをクリックする。  
<img src="https://gf6nxw.by.files.1drv.com/y4mw_gxGW-VU_3ck-iVibu4X2it9IgCCJhHNSg9DVn0go6n-V5Ftqmz_Smh5Pwvm5jotHxcGhBDX5sjATL4Ft6GWw8h5l53pMRUdQqfeaoQJ97TI5vl7XGA5rhpYW9Aoys-yYWY1ztszMD4SmhNCFSP7EQhQseQkrS_4GmvvXkMCfLhDsnTnoD0P7x3mlHFKrJYwr01nHfty8aH20YDTw6rfQ?width=1952&height=728&cropmode=none" width="600">
2. 「Slack API」画面が表示されたら、画面を下にスクロースして「Create a Slack app」ボタンをクリックする。
<img src="https://fq6pxw.by.files.1drv.com/y4mBpuRQP7jfSpRdrKZvvgl9xFL5s_Dv-aoND34ayDfOg9Xq0UdJaqPRcYIrNdX6GucVAttrLqeCIZMEhxw9Am9I9LFDoLZisiEZJEU5BQbPildd0vlvE2zTTnaFsiOkhKTFY5_NBLnW1gDICfyo_18p-z0SClYUTLd_wPWBaBc95oHID2G0MYWq-VP6a4ZTmz2tR4Am-5Ip68r6zEgwWZgQQ?width=1250&height=1228&cropmode=none" width="600">
3. 「App Name」に任意のアプリ名を入力し、「Development Slack Workspace」でご自身のSlack Workspaceを選択し、「Create App」ボタンで次に進む。
※ここではSlack Workspaceの作成方法を割愛させていただきます。
<img src="https://fv6hxw.by.files.1drv.com/y4m40jvCHa9ECSJknKL3r3BGG9ifc8E5c3rEfvCab1tWtg_rT_8XJ2u9heqOZUb8ySoxi1wAbbpUoy6VyO6kYWmYGSwynzGhqwqO4lsC5_PUVl8xFlYy-x_aSzNdRAgZKWn-u9HSeKzv84LXL4zAC3mtYIAknyrBaomUE03IGsnhBNOyOq4icdQLLZ9fA5mjcpVXf73KF3fH5RVSFW-inNyRg?width=1244&height=1018&cropmode=none" width="600">
4. 「Basic Information」画面が表示されたら、左側のメニューから「Bot Users」をクリックする。
<img src="https://fv6gxw.by.files.1drv.com/y4m7YtV0ngDwuaZV-bC425nDJaRdYcK_IvSYlis6HTLCYYWLoyhz1zT9EiXPf-PYC4WDa46WEUQ8q5Lue8BMRCzvqywACcoq0WmIVKyqN9SIXW3EkUJ9eyA7jRkrmyGIk5HzaMosWNRxPcktWNSnCItYhmeDk2LvNCew-9XmVwNK26DXBjoNqnjAYzSpIrBam3394OzqG4ezu0s_P88RBHbTQ?width=1270&height=1170&cropmode=none" width="600">
5. 「Bot User」画面で「Add a Bot User」をクリックする。  
<img src="https://fq6oxw.by.files.1drv.com/y4mi2RabPcPn5QT7Wb-K4hrSUcaKBs83B2fa3fPUFKPcqimnGpD-vSE3wvK_NzMWPUjHnYynYxs2nxlo6NhliRTKhCnPZE_GSW1ZpGs3Fvqqo7oLu7T4hQk44e224EI9uLQil9fSSozx2QQY3cCUw7WRc9hrg7v89YQ2L7kLi0f2nhGjh0N0jo_sWDkSYmTs4SUHpm_r9lu3JuKXVt2kVkFQQ?width=1680&height=744&cropmode=none" width="600">
6. 「Always Show My Bot as Online」を「On」にし、「Add Bot User」をクリックする。  
<img src="https://fq6nxw.by.files.1drv.com/y4mBg8kBoSqVBmJmaGu5Dck6M-3ZDqZchSbwRBJ2OUgsR9AjW2cNV6oUBfHX8e6QgeNh-aTcuO3Wh0NhXk8pOPYkUe7BzbX4W4-WuVDfsHLr1y1ooDLnIkSbYzMWoTW7CInpDvKcbMnlD7nyLzz7z_Jk0lzp_wsgr_5akZvrJ4Qq2WqBRPPC2Gs_5oNVDMkAedN0lmiS-vH20nHlSJYWu_hHQ?width=1532&height=1224&cropmode=none" width="600">

## 4-2 SlackとWatson Assistantの連携 (Connect Watson Assistant to Slack)
1. 左メニューの「Basic Information」をクリックし、下にスクロールして「App Credentials」セクションに表示されている「Verification Token」をコピーする。  
※**Credential**の情報は大切に管理してください。  
<img src="https://fq6mxw.by.files.1drv.com/y4m0ukPBfaFe0yOzeIXE0dEpma2xLKfeaOUaH3eDHuoCj7UAJNxNHeyqdDUstQzWTgG0h1-gt1pXlA1P2xwGBEK3WT08kSd81CYf1QwPAuAHrcLZL8dt6ZU4Eap04D3vb6f69pwRQHKO_DehdgONJ9Jx4VvmqA_Ip3SEbhYwqC5PQE0r3DNmbIUYuE7lP-OcYTgr6fa7rQM-mvrNs5M-Y8tDw?width=716&height=916&cropmode=none" width="600">
2. 「IBM Watson Assistant」画面に戻り「Configuration for Slack」のStep 2の「Verification toke」に貼り付ける。
<img src="https://gf6hxw.by.files.1drv.com/y4mvuvftx_vjMj6uKjjBgGYZ1GIDTjcLXhnWnRCLo7ULdaeWI3Z0A9rZBk0Atrwlvh4ezXk4i-UyZSrUWi8TN8gmHdfbikl4xYHVGfiCE2F4Zhekls5UH1Qbzfhw9nHo6aq5zXmxJqLCHXBNApyGX-WKtwL0JwQrACyN1i2lm7l1Ok3IudxoFzJyXNjvOlfmcHk5DyVaB_2QCTEn3bLg59L3g?width=1674&height=574&cropmode=none" width="600">
3. 「Slack API」サイトに戻り続いて左メニューの「OAuth & Permissions」より「Install App to Workspace」をクリックしてインストールする。
<img src="https://fv6pxw.by.files.1drv.com/y4mAvgg9ojmkN1T3ad5CbRupkNam8yLrRXz1PwF29lOXVbM-MJZQ6m8z4AHI8DYE11cE8QOp5FSO30WjXv1-K8zi_jo1JcZrDBHalqikGyVBCDypbNYPaSWmKzxIxFBIVbZqeDdIRxuMzUHd9Jm1PuyHU180Wgackfp_FyVBDUrM2oovlEODD5KH-bGt9ESRfbVCGlNMj4jQyEkmYMb2_jgww?width=1796&height=920&cropmode=none" width="600">
4. 確認画面が表示されたら内容を確認し「許可する」ボタンをクリックする。  
<img src="https://gf6gxw.by.files.1drv.com/y4mS1Hn84jRKl6_q0wykm3RrJyT2KXDk0qf9hbS_aZnpDRxrWmT6LorGWte62lluf3PFoE07_8A5c4InAm7PysSRwWgDTOwSMjkR_nhPuT3j9gu4sR_8mjfzrTk2_hxatgUxhABdt7_77a1zZCmSP0VMEnBH6_zegLRS6rR7a6SQYBIXnGnUKerWyI_AJ9IaYUFsI1MbWnPwv5OLuSEgygyMA?width=824&height=796&cropmode=none" width="500">
5. 生成された「OAuth Access Token」と「Bot User OAuth Access Token」をコピーしながら「IBM Watson Assistant」サイトに戻りStep 2のそれぞれのボックスに入力する。  
<img src="https://fv6nxw.by.files.1drv.com/y4mkEvKXS6-8XjBOMhM9zQGhjihXkkHgi_6EUSN6j05fQ3gcDCSCehTeyGZiOrXVTqJNOh1qYZkKaqGUzZmKuma85HcIj6NznKpBI6jG9-teeRFpOMbs-QvJTxIrU2rEJLS008d4CVT9jiHJ0C2j5ti1R-WWBUb7jWq4hFq_H3IiDeMrX98ETpSgbi9JA4AYn6rkI3TG3MSR8N-irCqK0trVg?width=2198&height=694&cropmode=none" width="600">

##4-3 Slack bot の設定
1. 「Slack API」サイトに戻り、「Event Subscriptions」の「Enable Event」を「On」にする。
<img src="https://fv6lxw.by.files.1drv.com/y4m5895ljxBOgwmv4HBKIB40kFVBabjC4IQd_p9ENJWT1v-OSe2T1TvHo_oU5r8cmiZgQbzjLf6yxyl0mLqaT1St0AvdW0Eq1gCLWjewXV3I_u51a-8jgxD35iPd33EzEI9ERQ5lmKa9ewcICYBFx83hHym-4CNLU4YxyWZQUPcue1F0IUHk6Y0BcqATvnBIgavXA66Q-Wo10Pme7nwfOnFMQ?width=1580&height=1090&cropmode=none" width="600">
2. 「IBM Watson Assistant」サイトのStep 3の「Configure your Slack bot」で「Generate request URL」をクリックし、生成されたURLをコピーする。
<img src="https://fv6mxw.by.files.1drv.com/y4mk3qH6qEsqtXjost6hkBenlDdhFCZw0j0ozlMysSHz1198pI0M7roP2M96ednsriSAwFNliJ4YyRJ5wf2Cn-ljgZglWvOnh8xO0o0RcGxotd6gOVv1vF4MhOEpeaztFpbQsL7JZVwu9fEVOCsvVV0-D8YPX9PUg0sUJz1Z_myVtnAVgCk0srB_jGUe-k51aloJuPoJb82o-dV2o8aOMrSMQ?width=1756&height=514&cropmode=none" width="600">
3. 「Slack API」サイトに戻り、「Request URL」を入力する。
※Verifiedと緑のチェックマークが表示されればOKです。
<img src="https://fv6kxw.by.files.1drv.com/y4m8zsJmRdytP1eUyFnnmhtz45E6dRu6zh4ZHxAQDbX6pFPmFlqKpZGD42vy8MPdsVHZ02sW2Ozy92lAE3kE8qAG_7VLcHBwkGN2PjSpP2aZhoBRUuSfxlpbFz80DMiah3gs9a9hjkOn9xgnMb2RQf27w1EXSeOQoQS7XOHGrLySobVvvFWz5d4eW3MnQPAHVSyzEfpFpPeCvEwwDWZ-s9IHA?width=1834&height=596&cropmode=none" width="600">

## 4-4 Assitantへの接続
1. 画面を下のほうへスクロールし、「Subscribe to Bot Events」の「Add Bot User Event」ボタンをクリックする。
<img src="https://fv6jxw.by.files.1drv.com/y4mtHfAofQ0a_7x1Trz_B4PnmxxA3xBnPM_9jDKeiZ7hGY75pqdX2Kw9XgAKy4pNJMQn0aGbWYywILJILUR9YIBV2VB8uMJZg55-K2Vbcfn6y1pNR-SLP8G-6VoyjrKvQOnfEZ_1Ag9sF0aQ4IkNtcKqvkW6phgOCHFhbHaHMqgXkWlqE70HNXF9SaWvTFhZ5_aTA6rCv5f5EbVoVKt9adoBQ?width=1504&height=772&cropmode=none" width="500">
2. ドロップダウンメニューより下記の2つのイベントを選択し、画面右下の「Save Changes」ボタンをクリックする。  
**message.im**  
**app_mention**  
<img src="https://fv6ixw.by.files.1drv.com/y4m3oIJdQeQp4-FjpNcxNgKWhtPmknyeyh9_zp-CH0-B3BKb9aXz9xzsfnDX6_0we7q8HzKjOkZ95wdDKwXRY-cStyxCmZ3RW_RwWQgTffUwgHR4Ing1XkgXZwmL67_WOlaB0xtGCw8yDA_gJgbTWWvSsDQp5DCXg_hRk6w39cdyEETerS_3zjv9MFE5Sq2FBdU684uYYoREdOgcK1YHHGjrQ?width=1544&height=1038&cropmode=none" width="600">
3. 「IBM Watsno Assitant」サイトで先ほど**4-3**の手順で生成した「Generated request URL」をコピーする。
4. 「Slack API」サイトの左側メニューの「Interactive Components」より「Interacitity」を「On」に変更する。
<img src="https://gf6ixw.by.files.1drv.com/y4mfcn5vEArV0zx-hc1IMROjcRTcL3y-RSI-UN2S54R2ADzgxx2jtwk5bQisSyP4Vsc_eMcw9S3rPyn7N-1STZr3S-HYto8z-vPa7e3DPrfkBVPy-akvEYsV2lZDIW7IfPXkx1hEN7fJTFhswyrzMAdFxLmRSaj_Ly1LJoavx4PKUurz2l9p7F7m-Pa7sKHvMS9map4SA5e0BGmg6QPnAPg4g?width=1784&height=1050&cropmode=none" width="600">
5. 「Interactivity」の「Request URL」を入力し「Save Changes」ボタンをクリックする。  
<img src="https://gf6jxw.by.files.1drv.com/y4mkwn3_FgIzk1id6H4jevh1g8pGGFrfpu5QTxFOHB679k10tMX0SuJxi1EaQBRdy-EGCS0AhQ0iy3rI3QEXhdna8yya7M1VcDgzcE2LU0ZmgyUgWVM-TJa6Wwr-aGNokntDBfDl-iJRCEMHgChGtR9nBsyeQjMCqojZ4368yweT5dFRGXxrx3hVFh-MYCk9oGS6k4Rp3jWIWYRa0zsrqnpgw?width=1406&height=688&cropmode=none" width="500">

# 5. Slack上で動作確認する
1. ご自身のSlack Workspaceへアクセスする
2. 「App」にご自身で作成されたアプリ名が表示されていることを確認する。
<img src="https://gf6kxw.by.files.1drv.com/y4mGZ_ose2omnH1mUn-HAI2z0gCukWkq8ZSEia9DhxbEzH268LPvOQ0uyGnFi86L6pgcVPbRR9XxIdW705MhfUbTi5_aOvru1rY4RvD6XMFhUJ7nnIovQ4AIzsR72fTMsNgBwtSJjBEEBneR9syUeg4d2bKFcqHZprszh8RtznIVhaZkSSKjaRyKQBWwuRm69OgxG2_78ny_MGwaIZ8HudOKQ?width=1986&height=1180&cropmode=none" width="600">
3. 何か話しかけてみる。  
(今回は英語のサンプルを用いているため、このSlack botが認識できるのは英語になります。)  
4. Slack botから応答が返ってきたら成功です！  
<img src="https://gf6lxw.by.files.1drv.com/y4m_kroX6J7NznF630sn55Blc3bkFZN_2dCmTo7JzKu3lUOpoH18IqMu1Z3JdGj5wtsWwnPbEP4qxD0hkKr9cZmThyGaYOf8gEWf4xhrELHvAPwm-54GuSPKLJQ9OjScGEIkKzr1zA3qBZgm15c1T-KfxWq-Ru19eJrJB8bLUAklNdmYt16B-_uc_Tcbbd8yi0HNjGgq2HnzrENXG2l0N32CQ?width=1366&height=592&cropmode=none" width="600">

以上です。後半はIBM Watson AssistantとSlack APIサイトを行ったり来たりの操作になりますが、入力ミスなどがなければスムーズに進めることができる内容だったかと思います。

【Note】
いづれのサービスの画面も2019年3月11日現在に取得したものです。今後予告なく変更される場合があります。ご了承ください。
