# enlarge
# 放大镜组件
### npm i yan-enlarge 
# Or 
### pnpm i yan-enlarge
# 传入一个图片src组成的数组
## 例：
<!-- 引入 -->
import Enlarge from 'yan-enlarge'
const imagesList = [
    'https://yanxuan-item.nosdn.127.net/ade0ec4f0d2d56c723becb8002a69f75.png',
    'https://yanxuan-item.nosdn.127.net/4c6a9c8a579b00e5e9c7b002d15a33a2.jpg',
    'https://yanxuan-item.nosdn.127.net/f832555ef368be44b530dfc4e70e96b8.jpg',
    'https://yanxuan-item.nosdn.127.net/e1c46f4d3ad7c0c4a511214a2756e2fc.jpg',
    'https://yanxuan-item.nosdn.127.net/e52eb92a519a268c4b6c54c4ad2bb95d.png',
]
<!-- 使用 -->
<enlarge :images="imagesList" />
