3/9(S)

3/8(S)

3/7
- 了解發生push時發生`error: RPC failed; HTTP 400 curl 22 The requested URL returned error: 400`的原因
  - 原因是push的檔案超過緩衝區大小，或者是網路訊號不好，最簡單的解法是拆開分成幾次push
  - push時 git 不會一個一個檔案即時送出，而是把多個檔案或變更合併到一個git物件，並放進緩衝區，再送到server
  - http.postBuffer是緩衝區的大小，http.postBuffer 預設值通常是 1048576  Byte (=1MB) [📗](https://git-scm.com/docs/git-config#Documentation/git-config.txt-httppostBuffer) [📗](https://git-scm.com/docs/gitfaq#Documentation/gitfaq.txt-WhatdoescodehttppostBuffercodereallydo)
  - 把http.postBuffer調大送給server的git物件也會變更大，所以調越大的話會導致push越慢 [📗](https://learn.microsoft.com/en-us/azure/devops/repos/git/rpc-failures-http-postbuffer?view=azure-devops)
    - 基於push會變慢，所以並不推薦修改http.postBuffer的值
  - 如果把http.postBuffer[調到超過server能接受的上限，那push還是會失敗](https://blog.miniasp.com/post/2014/09/07/Handle-large-Git-repository-on-Visual-Studio-Online)
  - server接受的檔案大小可以調整，但需要有權限，且不建議這麼做 [📗](https://docs.gitlab.com/topics/git/troubleshooting_git/#increase-the-post-buffer-size-in-git)
  - 檔案本身的大小不等於git物件的大小，因為git演算法會把檔案壓縮後變成git物件
  - `git config --get http.postBuffer` 可查看postBuffer大小，若無回傳值則代表為預設值

3/6
- 學習如何在Svelte專案設置default route [📗](https://svelte.dev/docs/kit/advanced-routing)
- 看standup show學英文 [📘](https://www.youtube.com/watch?v=0t8QCW78oDE)
  - That's messed up
    - A: That guy let his dog poop in front my door. He didn't even  clean it, he just left.
    - B: That's messed up.
  - tick someone off
    - I definitely get road rage. Once I start driving, a lot of things start to tick me off.

3/5
- 閱讀[橡果學院貼文](https://www.threads.net/@the.acorn.academy/post/DGxeAzZyZo5?xmt=AQGzXXUj_EAErEbaUiXTyZXJwqQ60Txv2xp8qNroyVQ1GJQ)
```
To即將要畢業找美商or海外工作的各位：
過去三天，我提供了幾大重點給大家，
給大家技巧上的建議還有心理建設，
前天講了履歷，昨天講Coffee Chat，
今天講英文面試，
明天會短暫回歸輕鬆小故事
這篇會專攻大家都適用的英文面試觀念，
會稍微籠統一點，
但我相信至少有一項會讓你覺得耳目一新
不要把這篇當作我的Google面試分享，
要看谷歌面試的話，去留言區看之前文章
-不管大家說什麼架構最棒，
其實來來去去都差不多，反正就是：
1-2句話講你的任務，
1-2句話講為什麼這件事很困難，
3-4句話講解決過程，1-2句話講結論，
1-2句話講你學到什麼，或是未來如何調整
（要詳細！看留言示範）
-只要有5個故事可以說，
基本上可以面對任何問題，
剩下的就是隨機應變去小調整，
我個人認為大家可以去查一下P&G八大問，
這八題都能回答的話，就完全沒問題了，
同一個故事可以回答好幾題
-儘量不要拿到面試了才準備，
尤其對我們英文非母語者來說，
要練到嘴巴腦袋都習慣英文，
是需要不少時間的，我之前還在上班的時候，
甚至會沒事去面試，練練手感

-如果你的英文程度在多益700以上的話，
英文面試強烈建議大家寫稿，
我知道大家都說，寫稿會限制你的發揮，
但最大原因是因為你寫了稿，
但沒有真的花很多時間把他變熟，
或是沒有人真的陪你練過，
自我介紹+五個故事，共六篇稿，
用AI三天一篇綽綽有餘，先不論完美不完美，
兩個禮拜就可以搞定
-大部分的外商其實對英文口說程度，
沒有真的很高的要求，
但如果是海外求職就真的要很好了，
除非能靠硬實力碾壓別人，但即使這樣，
很容易進去之後遇到天花板，
所以英文口說要加油，
我知道聽起來有點在販賣焦慮，
但某種程度上確實是，
要不然我就不會離開谷歌創業了，
對嚮往國際生活風格的人來說，
英文口說是硬需求
-英文口說要練到高低起伏的訣竅，
就是儘量讓你的句子短一點，每一個逗號都暫停，
每一個重點動詞、比較級形容詞、數字都加重音

什麼叫詳細，舉例：
不只要說
we created content that increase conversion rate
而且還要回答
what content, why this content, how did you come up with this content
又或者：
We believe that A is the better investment choice because they have lower risk.
還可以再加一點細節
A is the better investment choice because of their higher free cash flow, which can be a contingency if an event raises energy cost.
```

- 了解如何使用dev tool查看CSS animation [📗](https://developer.chrome.com/docs/devtools/css/animations?hl=zh-tw)


3/4
- 學到新的繪製半透明形狀，但不影響子元素的方法
  ```html
      <!-- 使用Tailwind的作法 -->
      <div id="parent" class="w-48 h-48 relative before:absolute before:top-0 before:left-0 before:content-[''] before:w-full before:h-full before:bg-blue-300 before:opacity-50">
          <p>child element</p>
      </div>
  ```

    相當於以下的手寫CSS

  ```css
      #parent {
          width: 12rem;
          height: 12rem;
          position: relative;
      }

      #parent::before {
          content: "";
          position: absolute;
          top: 0;
          left: 0;
          width: 100%;
          height: 100%;
          background-color: #93c5fd; /* Tailwind 的 bg-blue-300 */
          opacity: 50%;
      }
  ```

- 閱讀 [忙不是藉口，開不好 One-on-One 就是主管的問題](https://medium.com/@stevenyeh/%E5%BF%99%E4%B8%8D%E6%98%AF%E8%97%89%E5%8F%A3-%E9%96%8B%E4%B8%8D%E5%A5%BD-one-on-one-%E5%B0%B1%E6%98%AF%E4%B8%BB%E7%AE%A1%E7%9A%84%E5%95%8F%E9%A1%8C-bae77b0f466e)

3/3
- 了解IndexedDB [📗](https://developer.chrome.com/docs/apps/offline_storage)
    - 針對indexedDB的操作是非同步的
    - indexedDB的容量配額會根據瀏覽器有差異，當超過容量配額時先刪除哪些資料的標準也不同
        - `超過容量配額`時刪除資料的動作稱作`資料驅離`，localStorage、sessionStorage也有這個機制
    - 無痕模式下indexedDB容量配額會比較低
    - Safari是目前唯一有實作主動驅離資料的瀏覽器
        - [主動資料驅離](https://developer.mozilla.org/en-US/docs/Web/API/Storage_API/Storage_quotas_and_eviction_criteria#proactive_eviction)是指超過一定時間沒有操作網站的話，就把IndexedDB資料清除
- 了解如何用dev tool查看及變更 indexedDB 資料 [📗](https://developer.chrome.com/docs/devtools/storage/indexeddb?hl=zh-tw)

3/2(S)

3/1(S)

2/28
- 讀Svelte教學 ~Basic Svelte/Events/Spreading events [📗](https://svelte.dev/tutorial/svelte/spreading-events)
- 讀Svelte教學 ~Basic SvelteBindingsTextarea inputs [📗](https://svelte.dev/tutorial/svelte/textarea-inputs)
    - 當對select使用`bind:value`時要小心。當綁定初始化後，Svelte會自動將select的預設值設為option的第一個項目，而不是一直維持與之綁定的state的值

2/27
- 了解如何使用Svelte `bind:this` 取得DOM element [📗](https://svelte.dev/tutorial/svelte/bind-this)

2/26
試著在Svelte+Vite專案設定Graphql codegen

1. 安裝以下codegen套件
```
    // 用於GraphQL codegen產出type、schema
    "@graphql-codegen/typescript-graphql-request"
    "@graphql-codegen/cli"
    "@graphql-codegen/introspection"
    "@graphql-codegen/typescript-apollo-client-helpers"
    "@graphql-codegen/typescript-resolvers"
    "@parcel/watcher"

    // 用於fetch，且有plugin可以在codegen時產出document
    "graphql-request"

    // graphql-request的依賴
    "graphql-tag"
    "graphql"
```


2. 設定codegen config
   
  [設定檔可以用多種格式撰寫](https://the-guild.dev/graphql/codegen/docs/config-reference/codegen-config)
  ```ts
  // codegen.ts

  import { type CodegenConfig } from '@graphql-codegen/cli';

  const config: CodegenConfig = {
    schema: '你的GraphQL endpoint',
    documents: ['src/**/*.(svelte|ts|graphql)'],
    ignoreNoDocuments: true,
    // 每次執行codegen都把舊的檔案覆蓋
    overwrite: true,
    // 開啟watch模式，只要document有變動就會跑codegen
    watch: true,
    generates: {
      // codegen產出的type、document存放的位置
      './src/generated/graphql.ts': {
        plugins: [
          'typescript',
          'typescript-operations',
          '@graphql-codegen/typescript-graphql-request',
          'typescript-apollo-client-helpers',
          'typescript-resolvers',
        ],
      },
      // codegen產出的schema存放的位置
      './src/generated/graphql.schema.json': {
        plugins: ['introspection'],
      },
    },
  };

  export default config;
  ```

3. 在package.json新增script
  ```
  "scripts": {
      "dev": "yarn codegen & vite dev",
      "codegen": "graphql-codegen",
    },
  ```

4. 根據需求建立GraphQLClient集中管理headers之類的設定
  ```ts
  const apiClient = new GraphQLClient('你的GraphQL endpoint', {
    // 因為token可能會動態改變，所以headers需要定義為function
    headers: () => {
        const token = localStorage.getItem('key的名稱');

        return {
          // GraphQL的不論是query或mutation，method都是POST
          method: 'POST',
          authorization: `Bearer ${token}`,
        }
    },
      // 因為graphql-request沒有狀態管理功能，所以需要使用middleware和Svelte store製作API狀態管理
    requestMiddleware: async (request) => {
      apiStateManagementStore.set({
        isLoading: true,
      });
      return request;
    },
    responseMiddleware: async (response) => {
      if (response instanceof ClientError || response instanceof Error || response.errors) {
        apiStateManagementStore.set({
          isError: true,
        });
      }

      apiStateManagementStore.set({
        isLoading: false,
      });
    },
  });

  export default apiClient
  ```

2/25
- 閱讀 [Things only senior React engineers know](https://medium.com/@meric.emmanuel/things-only-senior-react-engineers-know-618d81154cb6)
  - 可以不用useEffect就不要用，尤其是在useEffect的callback中操作和UI有關的邏輯，因為會提高出現bug的風險
  - 當key prop的值改變時，會直接把整個element unmount，並mount一個新的element到DOM
  - 組件的children型別應該設為ReactNode，這樣才不會過度限縮彈性
    - ReactNode包含所有可以被渲染的東西，string、number、boolean、undefined、null、\<p>text<\/p>
    - ReactElement 則只有\<p>text<\/p>

2/24

2/23(S)

2/22(S)

2/21
- 學習一些更禮貌地說英文方式 [📘](https://www.youtube.com/watch?v=rQN4-l5AXE0)

|分類||例句|
| --- | --- | ---|
|請求|I was hoping you...|I was hoping you could help me.|
|請求|I don't suppose..., could you?|I don't suppose you could lend me a hand, could you?|
|表達意見| Aren't you kind of...| Aren't you kind of young to be getting marry?|
|討論|someone seems to...| You seem to have made a mistake here.|
|拒絕|I'm not sure I'll be able to...| I'm not sure I'll be able to make it to the meeting.|
|拒絕|It's looking unlikely that...|It's looking unlikely that we'll finish on time.|

2/20
- 學習一些更禮貌地說英文方式

|分類||例句|
| --- | --- | ---|
|請求 |I was wondering if... |I was wondering if you could do me a favor. |
|請求|Could I please ... | Could I please have your name? |
|請求|Do you mind if I...| Do you mind if I sit here? |
|請求|Would it be possible to...| Would it be possible to reschedule the meeting?|
|其他|By any chance| Are you, by any chance, available this weekend?|

2/19
- 在Svelte專案試用[shadcn-svelte](https://www.shadcn-svelte.com/)
  - Svelte的生態圈真的是比起React實在是小太多，簡直像是孤兒
  - 了解到新的選library的方式。可以看repo的最後一次commit時間距離當下多久
    - 如果是一個很新的repo最好在1~2個月以內
    - 已經算成熟的(ex: ajv)則半年左右都在允許範圍
    - 超成熟的(ex: lodash)則超過一年也行

2/18
- 讀Svelte教學 ~Basic Svelte/Logic/Await blocks [📗]([https://svelte.dev/tutorial/svelte/spread-props](https://svelte.dev/tutorial/svelte/await-blocks))
- 了解如何在AWS上設置一個純前端專案
  - S3
    - bucket
  - Cloudfront
    - distribution
      - error page
      - behavior
    - function
- 試著使用Github Actions做PR merge後自動部署到S3 bucket的dev folder

2/17
- 了解如何在Svelte專案設置formatOnSave功能 [📗](https://hoishing.medium.com/auto-format-svelte-in-vs-code-c0208c2010c9) [📗](https://github.com/sveltejs/prettier-plugin-svelte?tab=readme-ov-file)

2/16(S)
- 了解如何用Svelte store實作API狀態管理 [📗](https://www.youtube.com/watch?v=umnSLfR_VkM)
  - writable
  - readable
- 了解AbortController
  - 用於取消request  

2/15(S)

2/14
- 讀Svelte教學 ~Basic Svelte/Props/Spread props [📗](https://svelte.dev/tutorial/svelte/spread-props)

2/13
- 了解如何使用docker部署網站
  - 撰寫Dockerfile

  - 執行build image，並幫它打tag
    ```
    # -t 是tag的意思，用於幫image命名
    # image name 後方是指Dockerfile所在的目錄，.代表當前的目錄
    docker build --tag my-app .
    ```

    以上指令相當於以下多個指令
    ```
    docker build .
    docker image ls
    docker tag <image id> my-app
    ```

  - 把image 推到image儲存庫
    ```
    docker image push myrepo/my-app:latest
    ```
  - 在server上把image拉下來，並把它初始化變成一個容器(執行容器)
    ```
    docker image pull myrepo/my-app:latest
    ```

    ```
    # -d 是detach的意思，讓container在背景執行，不會佔用終端機
    # -p 是port的意思，將server的port 80連接container的port 3000
    # --name 後方是container的名字，可以省略
    # myrepo/my-app 是image的名字，即在步驟2中打的名稱
    docker container run -d -p 80:3000 --name hello123 myrepo/my-app
    ```

  - (optional) 根據需求在當下正在執行的container 設定環境變數
    ```
    # -e 是environment的意思，用於設定環境變數
    docker container run -e MY_ENV=production -e PORT=3000 myrepo/my-app
    ```
    之所以不直接在build image時就直接把環境變數包進去是因為這樣該image就跟特定環境綁定了，不能在多個環境複用

- 初步了解AWS的ECR服務
    - AWS的ECR是image的儲存庫，相當於私有的Docker Hub，Github也有提供私有image儲存庫的服務
    - 可和其他AWS 服務整合

2/12
- 看Docker快速入門教學[📗](https://www.youtube.com/watch?v=1wfgS31LcgQ&list=PLVVMQF8vWNCLsTAWVvGRyQP0ajj0Rx1--&index=2&t=20s)
  - 建立image的方式有2種
    - `docker build`
      - 用dockerfile是用於建立image
    - docker commit
      - 將image初始化成container，進行修改後再建立成另一個image
- 了解docker指令
  - docker指令有分新舊版，雖然舊版仍能使用，但推薦使用新的
  - 查看image
    ```
    # 本機所有的image
    # 舊版
    docker images
    # 新版
    docker image ls

    # 本機某個image
    docker images <image name>
    ```
  - 查看所有的container
    <img width="1017" alt="截圖 2025-02-11 下午6 15 35" src="https://github.com/user-attachments/assets/0cd9ac9f-837a-476c-89ed-e49150c4e40c" />
    ```
    # 舊版
    docker ps -a
    # 新版
    docker container ls
    ```
  - 移除image
    ```
    # 舊版
    docker rmi <image name>
    # 新版
    docker image rm <image name>
    ```
  - 移除container
    - image每次執行後就會產生一個container，如果用完不需要了可以把這些container刪掉
    ```
    # 舊版
    docker rm <container id或name>
    # 新版
    docker container rm <container id或name>
    ```

2/11
- 試試看在Windows11[安裝HyperV](https://www.youtube.com/watch?v=ExZIQj-DvI8)或WSL
  - 在Windows使用docker會需要它
  - 可以透過[官方文件](https://learn.microsoft.com/en-us/windows-server/virtualization/hyper-v/get-started/install-hyper-v?pivots=windows)內指示，使用shell command安裝
  - 可以照[影片](https://www.youtube.com/watch?v=ExZIQj-DvI8)的指示，來建立bat檔安裝
    <img width="739" alt="截圖 2025-02-10 下午6 02 33" src="https://github.com/user-attachments/assets/e7a047f8-72ee-4f20-baa1-6b7a858c704a" />
- 試試看在Windows11[安裝](https://docs.docker.com/desktop/setup/install/windows-install/)、啟動docker
  ![螢幕擷取畫面 2025-02-11 221118](https://github.com/user-attachments/assets/35d0e04f-947b-484a-a86a-e4bd1a79bf67)
  `啟動之後發現電腦效能太差，會導致風扇狂轉，所以刪除了，之後docekr的東西都只用Mac試`

2/10
- 試試看在Mac[安裝](https://docs.docker.com/desktop/setup/install/mac-install/)、啟動docker [📗](https://medium.com/%E5%AE%B8-%E5%AD%B8%E7%BF%92%E7%AD%86%E8%A8%98/mac-%E5%AE%89%E8%A3%9D-docker-%E5%8F%8A%E6%93%8D%E4%BD%9C%E6%8C%87%E4%BB%A4-6a9cfaa55979)
  - 安裝好桌面版之後，只要點兩下圖示就可以啟動docker
- 了解docker指令
  - 下載image
    - 指令
      ```
      # 舊版
      docker pull <image name>
      # 新版
      docker image pull <image_name>
      ```
      如果pull image時省略repo名，則預設會從Docker Hub拉取image
      如果是要從AWS ECR拉取image，則要在image名稱前加上ECR的網址還有repo名稱

    - docker應用程式下載
      <img width="1266" alt="截圖 2025-02-10 下午6 07 02" src="https://github.com/user-attachments/assets/4820d1f7-53e1-4d58-849c-0491c40febfb" />
      <img width="979" alt="截圖 2025-02-10 下午6 07 16" src="https://github.com/user-attachments/assets/6645bc53-3bff-4dba-8552-8e30e777f943" />
  - 搜尋想要使用的image
    - 指令
      ```
      docker search <image name>
      ```
    - 到[DockerHub](https://hub.docker.com/)搜尋
  - 執行image以產生container
    ```
    # 舊版
    docker run <image name>
    # 新版
    docker container run <image name>
    ```
2/9(S)
- 初步了解Docker [📗](https://www.youtube.com/watch?v=ZKdlglAxr7g)
  - Docker是一種實現容器化的工具
    - 容器化是指把應用程式跟它的依賴打包到一個獨立的環境。這個獨立的環境就是容器(container)
      - container初始狀態是映像檔(image)，透過指令執行image就會變成container
    - K8S是另一個目前主流的容器化工具
  - container具有一致性，可攜性、隔離性
    - 基於隔離性，容器內內只能放一種應用程式
 

2/8(S)

2/7
- 學習用於描述衝動行為、人的詞彙、片語 [📘](https://dictionaryblog.cambridge.org/2025/02/05/reckless-and-impulsive-acting-without-enough-thought/)
  - with no thought for something
    - He bought a expensive camera, with no thought for his financial condition.
  - hotheaded
  - [rash](https://www.thesaurus.com/browse/rash)
    - It was rash of him to buy such a expensive camera.
    - I think it was a bit rash of them to get married when they'd only known each other for a few weeks. (marry in haste, repent at leisure)
  - rush [headlong](https://www.thesaurus.com/browse/headlong) into something
    - She rushed headlong into marriage without really getting to know her partner.

2/6
- 了解React-Redux的connect function [📗](https://react-redux.js.org/api/connect)
  - connect function用於`連接class component和Redux的store`
  - connect接收mapStateToProps, mapDispatchToProps等參數，並回傳一個HOC(接受component並回傳component的function)
    - connect的內部有一段code可以取得store的值，再把store傳入mapStateToProps取得需要的某個屬性存入變數，再把變數當作props傳給傳入的component，這樣component就能和store連接起來了 [🖌](https://codesandbox.io/p/sandbox/redux-zombie-child-component-problem-5h34q5?file=%2Fsrc%2FHOC%2Fconnect.js%3A5%2C37-5%2C42)

2/5
- 聽Johnny Stimson的You can do it 學英文 [📘](https://www.youtube.com/watch?v=L2ADdk3w-rg&list=RDMM&index=4)
  - put your heart into something/put your heart and soul into something (全心投入)
  - brush someting off (拍掉、刷掉)
    - I brushed the dirt off my shoes.
  - It is a part of life. (表達某件事情是人生中不可避免的經歷，無論是好是壞。通常用來安慰別人，或者表達一種對人生的理解)
    - Failure is a part of life.

2/4
- 了解mapStateToProps [📗](https://www.dhiwise.com/post/mapstatetoprops-or-useselector-a-quick-comparison)
  - mapStateToProps是配合Redux使用的一種function，它是connect component的一部分，用於取得store
    - mapStateToProps會把整個store中的某個屬性當作props往下傳，而useSelector則是訂閱store的部分屬性，所以後者re-render次數會較少，故效能較好
  - 最早推出是為了`配合class component使用`，已經成為一種古早味設計模式
    - function component出了以後，Redux也推出功能類似的useSelector來搭配它
    - `不要跟function component一起用，會導致zombie child component`

2/3
- 了解stacking context [📗](https://ithelp.ithome.com.tw/articles/10217945)
  - stacking context是指使用positioned box建立的環境堆疊，可以透過以下CSS屬性建立
    ```css
    position: fixed;
    
    position: sticky;
    
    position: relative;
    z-index:100;

    position: absolute;
    z-index:100;

    transform: translate(100px, 100ox);

    /* 只要小於1就可以 */
    opacity: 0.9;
    ```
  - stacking context內的元素不會觸發[reflow](https://github.com/tempura327/learning-diary/blob/master/2024/README.md#1121)
  - 位於不同stacking context的元素間不會互相比較z-index

- n8n[📗](https://github.com/n8n-io/n8n)
